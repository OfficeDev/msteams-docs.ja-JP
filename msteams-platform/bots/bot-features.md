---
title: ボットと SDK
author: surbhigupta
description: ボットを構築するためのツールと SDK のMicrosoft Teamsです。
ms.topic: overview
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: 5a95159df887033bca339efd871261938aecb07d
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453888"
---
# <a name="bots-and-sdks"></a>ボットと SDK

次のいずれかのツールまたは機能を使用して、Microsoft Teamsで動作するボットを作成できます。

* [Microsoft Bot Framework SDK](#bots-with-the-microsoft-bot-framework)
* [Power Virtual Agents](#bots-with-power-virtual-agents)
* [仮想アシスタント](~/samples/virtual-assistant.md)
* [Webhook とコネクタ](#bots-with-webhooks-and-connectors)

## <a name="bots-with-the-microsoft-bot-framework"></a>ボットとMicrosoft Bot Framework

ユーザー Teamsボットは、次の要素で構成されます。

* ユーザーがホストする一般にアクセス可能な Web サービス。
* Web サービスのボット フレームワーク登録。
* Web Teamsクライアントを接続するアプリ Teamsパッケージ。

> [!TIP]
> 開発者ポータルを使用して、Web サービスをボット フレームワークに登録し、アプリ構成を指定します。 詳細については、「開発者ポータル[で](~/concepts/build-and-test/teams-developer-portal.md)アプリを管理する」を参照Teams。

ボット [フレームワークは、](https://dev.botframework.com/) ボット フレームワーク、C#、Python、および JavaScript をJavaする豊富な SDK です。 ボット フレームワークに基づくボットが既に存在する場合は、ボット フレームワークで動作するボットを簡単にTeams。 SDK をC#、Node.jsを使用[します。](/microsoftteams/platform/#pivot=sdk-tools) これらのパッケージは、基本的な Bot Builder SDK のクラスとメソッドを次のように拡張します。

* コネクタ カードのような特殊なカードOffice 365使用します。
* アクティビティTeams固有のチャネル データを設定します。
* メッセージング拡張要求を処理する。

> [!IMPORTANT]
> Web プログラミング テクノロジTeamsアプリを開発し、[Bot Framework REST API を直接呼び出](/bot-framework/rest-api/bot-framework-rest-overview)します。 ただし、すべてのケースでトークン処理を実行する必要があります。

## <a name="bots-with-power-virtual-agents"></a>ボットとPower Virtual Agents

[Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents)は、Microsoft Power プラットフォームとボット フレームワーク上に構築されたチャットボット サービスです。 Power Virtual Agent 開発プロセスでは、ガイド付き、コードなし、グラフィカル インターフェイスのアプローチを使用して、チーム メンバーがインテリジェントな仮想エージェントを簡単に作成および維持できます。 ポータルでチャットボットを作成[Power Virtual Agents、](https://powervirtualagents.microsoft.com)チャットボットと簡単に統合[Teams](how-to/add-power-virtual-agents-bot-to-teams.md)。 開始方法の詳細については、「ドキュメント」[をPower Virtual Agentsしてください](/power-virtual-agents)。

>[!NOTE]
>Microsoft Power Platform を使用して、アプリ ストアに発行するアプリを作成Teams必要があります。 Microsoft Power Platform アプリは、組織のアプリ ストアにのみ発行できます。

## <a name="bots-with-webhooks-and-connectors"></a>Webhooks とコネクタを持つボット

Webhooks とコネクタは、ボットを Web サービスに接続します。 Webhooks とコネクタを使用すると、ワークフローや他の簡単なコマンドの作成など、基本的な操作を行う簡単なボットを作成できます。 これらは、作成したチームでのみ使用できます。会社のワークフローに固有の単純なプロセスを対象とします。 詳細については、「 [webhooks とコネクタの機能」を参照してください](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)。

## <a name="advantages-of-bots"></a>ボットの利点

Microsoft Teams のボットは、1 対 1 の会話、グループ チャット、チーム内のチャネルで扱うことができます。 各スコープは、会話ボットに固有の機会と課題を提供します。

| チャネル | グループ チャット | 1 対 1 のチャット |
| :-- | :-- | :-- |
| 大規模なリーチ | メンバーの数が少ない | 従来の方法 |
| 個々の対話を簡潔に | @mentionボットへのアクセス  | Q&ボット |
| @mentionボットへのアクセス | チャネルに似ている | ジョークを伝え、メモを取るボット |

### <a name="in-a-channel"></a>チャネル

チャネルには、最大 2,000 人までの複数のユーザー間のスレッド会話が含まれる。 これにより、ボットに大量のリーチが生まれる可能性がありますが、個々のやり取りは簡潔である必要があります。 従来のマルチターン操作は機能しません。 代わりに、対話型カードまたはタスク モジュールを使用するか、会話を 1 対 1 の会話に移動して多くの情報を収集する必要があります。 ボットにはメッセージへのアクセスのみ許可されます `@mentioned`。 Microsoft Graphレベルのアクセス許可を使用して、会話から追加のメッセージを取得できます。

ボットは、次の場合にチャネルで優れた機能を提供します。

* 通知: ユーザーが追加情報を取得する対話型カードを提供します。
* アンケートやアンケートなどのフィードバック シナリオ。
* 単一の要求または応答サイクルは対話を解決し、結果は会話の複数のメンバーに役立ちます。
* ソーシャルボットや楽しいボット。素晴らしい猫の画像を取得し、ランダムに勝者を選ぶなどです。

### <a name="in-a-group-chat"></a>グループ チャット

グループ チャットは、3 人以上のユーザー同士で行われる非スレッドの会話です。 チャネルよりもメンバーは少なく、一時的な会話が多いのが特徴です。 チャネルと同様に、ボットはメッセージに直接アクセスできるのみです `@mentioned` 。

チャネルでボットがうまく機能する場合は、グループ チャットの方がうまく機能します。

### <a name="in-a-one-to-one-chat"></a>1 対 1 のチャット

1 対 1 のチャットは、会話ボットがユーザーと対話する従来の方法です。 1 対 1 の会話型ボットの例を次に示します。

* Q&ボット
* 他のシステムでワークフローを開始するボット
* ジョークを伝えるボット
* メモを取るボット 1 対 1 のチャットボットを作成する前に、会話ベースのインターフェイスが機能を提示する最善の方法かどうかを検討してください。

## <a name="disadvantages-of-bots"></a>ボットの欠点

ボットとユーザーの間の広範なダイアログは、タスクを完了するための低速で複雑な方法です。 過剰なコマンド、特に広範なコマンドをサポートするボットは、ユーザーが成功または肯定的に表示されません。

### <a name="have-multi-turn-experiences-in-chat"></a>チャットでのマルチターン エクスペリエンス

広範なダイアログでは、開発者が状態を維持する必要があります。 この状態を終了するには、ユーザーがタイム アウトするか、[キャンセル] を選択する必要 **があります**。 また、このプロセスは時間のかかっています。 たとえば、次の会話シナリオを参照してください。

ユーザー: Megan との会議をスケジュールして。

ボット: 200 件の結果が見つかりました。苗字と名前を含めてください。

ユーザー: Megan Bowen との会議をスケジュールして。

ボット: かしこまりました。Megan Bowen との会議を何時にご希望ですか?

ユーザー: 午後 1 時に。

ボット: 何日のですか?

### <a name="support-too-many-commands"></a>多くのコマンドをサポートする

現在のボット メニューには 6 つのコマンドしか表示されないので、それ以上のコマンドを頻度で使用する可能性は低い。 幅広いアシスタントの仕事と運賃を向上させようとするのではなく、特定の領域に深く入り込むボット。

### <a name="maintain-a-large-knowledge-base"></a>大規模なナレッジ ベースを維持する

ボットの欠点の 1 つは、応答が未確認の大規模な取得ナレッジ ベースを維持することは困難である点です。 ボットは、短く迅速なやり取りに最適で、回答を探している長いリストをふるいにかけない。

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

|サンプルの名前 | 説明 | .NETCore | Node.js |
|----------------|-----------------|--------------|----------------|
| Teams 会話ボット | メッセージングおよび会話イベントの処理。 |[表示](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[表示](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot)|

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [ボットのアクティビティ ハンドラー](~/bots/bot-basics.md)

## <a name="see-also"></a>関連項目

* [通話と会議のボット](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)
* [ボットの会話](~/bots/how-to/conversations/conversation-basics.md)
* [ボット コマンド メニュー](~/bots/how-to/create-a-bot-commands-menu.md)
* [サーバー内のボットの認証フロー Microsoft Teams](~/bots/how-to/authentication/auth-flow-bot.md)
* [ボットでタスク モジュールを使用する](~/task-modules-and-cards/task-modules/task-modules-bots.md)
