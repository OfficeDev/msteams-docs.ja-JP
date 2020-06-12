---
title: 会話ボットとは
author: clearab
description: Microsoft Teams の会話ボットの概要。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 140be426ac789efbf044130b0683f60af9f617d6
ms.sourcegitcommit: b822584b643e003d12d2e9b5b02a0534b2d57d71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/11/2020
ms.locfileid: "44704468"
---
# <a name="what-are-conversational-bots"></a>会話ボットとは

会話ボットを使用すると、ユーザーは、テキスト、対話型カード、タスク モジュールで Web サービスとのやり取りができるようになります。 会話型ボットの機能は非常に柔軟性があり、単純なコマンドだけでなく、複雑で人工知能を搭載した自然言語処理の仮想アシスタントを処理できるようにスコープを設定することができます。 大規模なアプリケーションはもちろん、スタンドアロンのものにも適用することができます。

以下の GIF は、テキストと対話型カードの両方を使用して、1 対 1 のチャットのボットで会話しているユーザーを示しています。 カード、テキスト、タスク モジュールを適切に組み合わせることが、便利なボットを作成するための鍵となります。 ボットでテキスト以上のことができるようになります。

![FAQ プラス GIF](~/assets/images/FAQPlusEndUser.gif)

## <a name="build--a-bot-for-teams-with-the-microsoft-bot-framework"></a>Microsoft Bot フレームワークを使用して Teams 用の bot を構築する

[Microsoft Bot フレームワーク](https://dev.botframework.com/)は、C#、Java、Python、JavaScript を使用してボットを作成するための豊富な SDK です。 Bot Framework に基づくボットが既にある場合は、簡単な操作でそのボットを Microsoft Teams で動作するように適応させることができます。 用意されている [SDK](/microsoftteams/platform/#pivot=sdk-tools) を活用するため、C# か Node.js を使用することをお勧めします。 これらのパッケージは、基本的な Bot Builder SDK のクラスとメソッドを次のように拡張します。

* Office 365 コネクタ カードなどの専用のカードを使用する。
* アクティビティに関する Teams 固有のチャネル データを使用して設定する。
* メッセージング拡張要求を処理する。

Teams ボットは次の 3 つ要素で構成されています。

* お客様がホストし、公開している Web サービス。
* Bot Framework へのボットの登録。
* アプリ マニフェストを含む Teams アプリ パッケージ。 これは、ユーザーがインストールするもので、Bot Service 経由でルーティングされ、Teams クライアントをお客様の Web サービスに接続します。

> [!IMPORTANT]
> 任意の Web プログラミング技術で Teams アプリを開発し、[Bot Framework REST API](/bot-framework/rest-api/bot-framework-rest-overview) を直接呼び出すことができますが、すべてのトークン処理を自分で実行する必要があります。

> [!TIP]
> Teams App Studio を使用すると、アプリ マニフェストを作成して構成でき、Web サービスを Bot Framework のボットとして登録できます。 また、React 制御ライブラリと、対話型カードのビルダーも用意されています。 「[Teams App Studio を使う](~/concepts/build-and-test/app-studio-overview.md)」を*参照してください*。

## <a name="create-a-chatbot-for-teams-with-microsoft-power-virtual-agents"></a>Microsoft Power Virtual Agent を使用して Teams の chatbot を作成する

[パワー仮想エージェント](/power-virtual-agents/fundamentals-what-is-power-virtual-agents)は、Microsoft Power Platform および Bot フレームワーク上に構築された chatbot サービスです。  パワー仮想エージェントの開発プロセスでは、コード化されていないグラフィカルインターフェイスアプローチを使用して、チームのすべてのメンバーがインテリジェントな仮想エージェントを簡単に作成および管理できるようにします。  [Power Virtual agents ポータル](https://powervirtualagents.microsoft.com)で chatbot を作成したら、 [power virtual agents Chatbot と Teams](how-to/add-power-virtual-agents-bot-to-teams.md)を簡単に統合することができます。 パワー仮想エージェント chatbot の作成を開始するには、[パワー仮想エージェントのドキュメント](https://docs.microsoft.com/power-virtual-agents/)を*参照してください*。

## <a name="webhooks-and-connectors"></a>Webhook とコネクタ

Webhook とコネクタを使用すると、ワークフローやその他の単純なコマンドの開始など、基本的なやり取りを行うためのシンプルなボットを作成することができます。 これらのユーザーは、ボットが作成されたチーム内にのみ存在し、会社のワークフロー固有の基本プロセスでのみ利用することができます。 詳細については、「[Webhook とコネクタとは](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)」を*参照してください*。

## <a name="where-bots-work-best"></a>ボットが最適に動作するケース

Microsoft Teams のボットは、1 対 1 の会話、グループ チャット、チーム内のチャネルで扱うことができます。 各スコープに、会話ボット向けの機能と条件があります。

### <a name="in-a-channel"></a>チャネル

チャネルでは、複数のユーザー間のスレッド形式の会話が扱われます。多くのユーザー同士 (現在は最大 2000) で会話が行われる場合もあります。 これにより、ボットが大規模になる可能性がでてきますが、それぞれの対話を簡潔にする必要があります。 ただし、従来の複数ターンの対話は、うまく動作しない可能性があります。 多くの情報を収集する必要がある場合は、対話型カードまたはタスク モジュールを使用するか、1 対 1 の会話に変更することをお勧めします。 Bot は、 `@mentioned` Microsoft Graph を使用して会話から他のメッセージを取得することもできますが、組織レベルの昇格されたアクセス許可を使用してメッセージを取得することができます。

ボットの利点をチャネル内で活用できるシナリオは以下のとおりです。

* **通知** (特にユーザーが追加情報を取得するための対話型カードを提供する場合)。
* 投票やアンケート調査などの**フィードバック シナリオ**。
* **単一の要求/応答サイクル**で解決できる対話。複数のメンバーで会話をする場合にこれが役立ちます。
* **交流/娯楽を目的としたボット** — 面白い猫の画像を取得したり、勝者をランダムに選んだりします。

### <a name="in-a-group-chat"></a>グループ チャット

グループ チャットは、3 人以上のユーザー同士で行われる非スレッドの会話です。 チャネルよりもメンバーは少なく、一時的な会話が多いのが特徴です。 チャネルと同様に、ボットは `@mentioned` のメッセージにのみに直接アクセスできます。

通常、チャネルで正常に動作するシナリオは、グループ チャットでも同様に機能します。

### <a name="in-a-one-to-one-chat"></a>1 対 1 のチャット

これは、会話ボットがユーザーとやり取りする従来の方法です。 これにより、さまざまなワークロードを実現できます。 Q&A ボット、別のシステムでワークフローを開始するボット、ジョークを言うボット、メモを取るボットなどがありますが、これらはごく一部です。 機能を表示するための方法として、会話ベースのインターフェイスが最適な方法であるかどうかを必ず検討します。

## <a name="bot-fails"></a>ボットが不適切なケース

### <a name="having-multi-turn-experiences-in-chat"></a>チャットで複数回やり取りが交わされる場合

ボットとユーザーが対話を長く続けると、タスクの完了に要する時間が長くなり、必要以上に複雑になります。また、開発者は状態を維持することが必要になります。 このような状態を終了するには、ユーザーはタイムアウトするか、「*Cancel*」と入力する必要があります。 何より、この処理は不必要なほど長々しいものになります。

ユーザー: Megan との会議をスケジュールして。

ボット: 200 件の結果が見つかりました。苗字と名前を含めてください。

ユーザー: Megan Bowen との会議をスケジュールして。

ボット: かしこまりました。Megan Bowen との会議を何時にご希望ですか?

ユーザー: 午後 1 時に。

ボット: 何日のですか?

### <a name="supporting-too-many-commands"></a>サポートすべきコマンドが多すぎる場合

サポートするコマンドがあまりに多く、特に広範な種類に及ぶボットは、うまく機能しないことや、ユーザーからの評価が低くなる傾向があります。 現在のボット メニューにはコマンドが 6 つしか表示されないため、それ以外のコマンドは滅多に使用されなくなります。 幅広いアシストを提供するボットより、特定の分野を深く掘り下げるボットの方がうまくいきます。

### <a name="maintaining-a-large-retrieval-knowledge-base-with-unranked-responses"></a>ランクが未設定の応答を使用した大規模な情報入手ナレッジ ベースの維持

Bot は、短時間で簡単にやり取りするのに最も適しています。これは、sifting ではなく、回答を探すために長いリストを使用しています。

## <a name="get-started"></a>作業の開始

* [C#/dotnet での Teams 会話ボット](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot)
* [JavaScript での Teams 会話ボット](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot)

## <a name="learn-more"></a>詳細情報

> [!div class="nextstepaction"]
> [Teams でのボットの基本](~/bots/bot-basics.md)

> [!div class="nextstepaction"]
> [Teams のボットを作成する](~/bots/how-to/create-a-bot-for-teams.md)
