---
title: 会話ボットとは
author: clearab
description: Microsoft Teams の会話ボットの概要。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 7bde886b67788a355181c83287d999a3bfb9727a
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674746"
---
# <a name="what-are-conversational-bots"></a>会話ボットとは

会話ボットを使用すると、ユーザーは、テキスト、対話型カード、タスク モジュールで Web サービスとのやり取りができるようになります。 会話型ボットの機能は非常に柔軟性があり、単純なコマンドだけでなく、複雑で人工知能を搭載した自然言語処理の仮想アシスタントを処理できるようにスコープを設定することができます。 大規模なアプリケーションはもちろん、スタンドアロンのものにも適用することができます。

以下の GIF は、テキストと対話型カードの両方を使用して、1 対 1 のチャットのボットで会話しているユーザーを示しています。 カード、テキスト、タスク モジュールを適切に組み合わせることが、便利なボットを作成するための鍵となります。 ボットでテキスト以上のことができるようになります。

![FAQ プラス GIF](~/assets/images/FAQPlusEndUser.gif)

## <a name="what-tasks-are-best-handled-by-bots"></a>ボットによって最適に処理されるタスク

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

## <a name="how-do-bots-work"></a>ボットの機能

ボットは、以下の 3 つで構成されています。

* ホストをして、公開している Web サービス。
* ボット登録 (Bot Framework にボットを登録する)。
* アプリ マニフェストを含む Teams アプリ パッケージ。 これは、ユーザーがインストールし、Teams クライアントを Web サービスに接続 (Bot Service を経由してルーティング) します。

Microsoft Teams のボットは、[Microsoft Bot Framework](https://dev.botframework.com/)に基づいて構築されています。 (Bot Framework に基づくボットが既にある場合は、そのボットを Microsoft Teams での動作に容易に適応させることができます)。[SDK](/microsoftteams/platform/#pivot=sdk-tools) を利用するには、C# か Node.js のどちらかを使用することをお勧めします。 これらのパッケージは、以下の基本的な Bot Builder SDK のクラスとメソッドを拡張します。

* Office 365 コネクタ カードなどの専用のカードの使用。
* アクティビティに関する Teams 固有のチャネル データの使用と設定。
* メッセージング拡張要求の処理。

> [!IMPORTANT]
> 任意の Web プログラミング技術で Teams アプリを開発し、[Bot Framework REST API](/bot-framework/rest-api/bot-framework-rest-overview) を直接呼び出すことができますが、すべてのトークン処理を自分で実行する必要があります。

*Teams App Studio* を使用すれば、アプリ マニフェストの作成と構成を行うことができ、Web サービスを Bot Framework のボットとして登録することができます。 また、React 制御ライブラリと、対話型カードのビルダーも用意されています。 「[Teams App Studio を使う](~/concepts/build-and-test/app-studio-overview.md)」を*参照してください*。

## <a name="webhooks-and-connectors"></a>Webhook とコネクタ

Webhook とコネクタを使用すると、ワークフローやその他の単純なコマンドの開始など、基本的なやり取りを行うためのシンプルなボットを作成することができます。 これらのユーザーは、ボットが作成されたチーム内にのみ存在し、会社のワークフロー固有の基本プロセスでのみ利用することができます。 詳細については、「[Webhook とコネクタとは](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)」を*参照してください*。

## <a name="get-started"></a>作業の開始

* [C#/dotnet での Teams 会話ボット](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot)
* [JavaScript での Teams 会話ボット](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot)

## <a name="learn-more"></a>詳細情報

* [Teams でのボットの基本](~/bots/bot-basics.md)
* [Teams のボットを作成する](~/bots/how-to/create-a-bot-for-teams.md)
