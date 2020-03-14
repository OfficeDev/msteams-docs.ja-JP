---
title: 会話ボットとは
author: clearab
description: Microsoft Teams の会話ボットの概要。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: e10275cba97f835cd59e572b48d2db7cb902d096
ms.sourcegitcommit: fdcd91b270d4c2e98ab2b2c1029c76c49bb807fa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "42635306"
---
# <a name="what-are-conversational-bots"></a>会話ボットとは

会話ボットを使用すると、ユーザーは、テキスト、対話型カード、タスク モジュールで Web サービスとのやり取りができるようになります。 これらは非常に柔軟になっており、話し言葉の bot は、いくつかの簡単なコマンドまたは複雑で人為的に処理される、自然言語の仮想アシスタントを処理するようにスコープを設定できます。 大規模なアプリケーションの1つの側面、または完全にスタンドアロンにすることができます。

以下の GIF は、テキストと対話型カードの両方を使用して、1 対 1 のチャットのボットで会話しているユーザーを示しています。 カード、テキスト、タスク モジュールを適切に組み合わせることが、便利なボットを作成するための鍵となります。 ボットでテキスト以上のことができるようになります。

![FAQ プラス GIF](~/assets/images/FAQPlusEndUser.gif)

## <a name="how-bots-work"></a>Bot のしくみ

Teams の bot は3つの要素で構成されます。

* ホストをして、公開している Web サービス。
* Bot が Bot フレームワークに登録されます。
* アプリマニフェストを含む Teams アプリパッケージ。 これは、ユーザーがインストールし、チームクライアントを Bot サービスを経由して web サービスに接続することです。

Microsoft Teams のボットは、[Microsoft Bot Framework](https://dev.botframework.com/)に基づいて構築されています。 Bot フレームワークに基づく bot が既にインストールされている場合は、それを Microsoft Teams での動作に容易に適応させることができます。 [Sdk](/microsoftteams/platform/#pivot=sdk-tools)を利用するには、C# または node.js のどちらかを使用することをお勧めします。 これらのパッケージは、基本的な Bot ビルダー SDK のクラスとメソッドを次のように拡張します。

* Office 365 コネクタカードなどの専用カードの種類を使用します。
* アクティビティのチーム固有のチャネルデータを使用して設定します。
* メッセージング拡張要求を処理します。

> [!IMPORTANT]
> 任意の Web プログラミング技術で Teams アプリを開発し、[Bot Framework REST API](/bot-framework/rest-api/bot-framework-rest-overview) を直接呼び出すことができますが、すべてのトークン処理を自分で実行する必要があります。

> [!TIP]
> Teams アプリ Studio * を使用すると、アプリマニフェストを作成して構成し、web サービスを bot フレームワーク上の bot として登録できます。 また、React 制御ライブラリと、対話型カードのビルダーも用意されています。 「[Teams App Studio を使う](~/concepts/build-and-test/app-studio-overview.md)」を*参照してください*。

## <a name="webhooks-and-connectors"></a>Webhook とコネクタ

Webhook とコネクタを使用すると、ワークフローやその他の単純なコマンドの開始など、基本的なやり取りを行うためのシンプルなボットを作成することができます。 これらのユーザーは、ボットが作成されたチーム内にのみ存在し、会社のワークフロー固有の基本プロセスでのみ利用することができます。 詳細については、「[Webhook とコネクタとは](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)」を*参照してください*。

## <a name="where-bots-work-best"></a>Bot の最適な動作

Microsoft Teams のボットは、1 対 1 の会話、グループ チャット、チーム内のチャネルで扱うことができます。 各スコープに、会話ボット向けの機能と条件があります。

### <a name="in-a-channel"></a>チャネル

チャネルでは、複数のユーザー間のスレッド形式の会話が扱われます。多くのユーザー同士 (現在は最大 2000) で会話が行われる場合もあります。 これにより、ボットが大規模になる可能性がでてきますが、それぞれの対話を簡潔にする必要があります。 ただし、従来の複数ターンの対話は、うまく動作しない可能性があります。 多くの情報を収集する必要がある場合は、対話型カードまたはタスク モジュールを使用するか、1 対 1 の会話に変更することをお勧めします。 ボットは `@mentioned` のメッセージにのみ直接アクセスできますが、Microsoft Graph および組織レベルの引き上げられたアクセス許可を使用して、会話から追加のメッセージを取得することはできません。

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

## <a name="bot-fails"></a>Bot が失敗する

### <a name="having-multi-turn-experiences-in-chat"></a>チャットでの複数ターンエクスペリエンス

Bot とユーザーの間の広範なダイアログは、タスクを完了するための低速で複雑な方法であり、開発者が状態を維持する必要もあります。 この状態を終了するには、ユーザーはタイムアウトまたは「*キャンセル*」と入力する必要があります。 すべてのプロセスは、不必要に面倒です。

ユーザー: Megan を使用して会議をスケジュールします。

BOT: 200 の結果が見つかった場合は、姓と名を含めるようにしてください。

ユーザー: Megan Bowen を使用して会議をスケジュールします。

BOT: Megan Bowen とどのような時間を使用しますか?

ユーザー: 1:00 pm。

BOT: どちらの日になりますか?

### <a name="supporting-too-many-commands"></a>サポートするコマンドの数が多すぎる

特に広範なコマンドをサポートしているボットは、ユーザーによって成功または肯定されることはありません。 現在の bot メニューに表示されるコマンドは6つだけなので、どのような頻度でも使用される可能性はほとんどありません。 広範なアシスタントではなく、特定の地域に深く関係している bot は、fare に適しています。

### <a name="maintaining-a-large-retrieval-knowledge-base-with-unranked-responses"></a>ランク付けされていない応答を持つ大規模な取得ナレッジベースを維持する

Bot は短時間ですばやく対話するのに適していますが、sifting では、回答を検索するのに長いリストは含まれていません。

## <a name="get-started"></a>作業の開始

* [C#/dotnet での Teams 会話ボット](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot)
* [JavaScript での Teams 会話ボット](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot)

## <a name="learn-more"></a>詳細情報

> [!div class="nextstepaction"]
> [Teams でのボットの基本](~/bots/bot-basics.md)

> [!div class="nextstepaction"]
> [Teams のボットを作成する](~/bots/how-to/create-a-bot-for-teams.md)
