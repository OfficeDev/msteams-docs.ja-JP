---
title: ボットと SDK
author: clearab
description: Microsoft Teams のボットと SDK。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: b38a40cfd88c9b5879f6d777f50b919125ce9ec9
ms.sourcegitcommit: dd2220f691029d043aaddfc7c229e332735acb1d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2021
ms.locfileid: "51995975"
---
# <a name="bots-and-sdks"></a>ボットと SDK

Microsoft Teams で動作するボットを作成するには、次のいずれかを使用できます。
* Microsoft Bot Framework SDK 上に構築された既存のボット。
* Power Virtual Agents chatbot Service。
* Webhooks とコネクタ。

## <a name="bots-and-the-microsoft-bot-framework"></a>ボットと Microsoft Bot Framework

Teams ボットは、次の 3 つの要素で構成されます。

* お客様がホストし、公開している Web サービス。
* Bot Framework へのボットの登録。
* アプリ マニフェストを含む Teams アプリ パッケージ。 これは、ユーザーが Teams クライアントをインストールし、ボット サービス経由でルーティングされる Web サービスに接続する方法です。

ボット [フレームワークは、](https://dev.botframework.com/) カスタム スクリプト、C#、Python、および JavaScript をJavaボットを作成するために使用される豊富な SDK です。 ボット フレームワークに基づくボットが既にある場合は、Microsoft Teams で動作するボットを簡単に変更できます。 SDK を利用C#またはNode.jsを使用 [します](/microsoftteams/platform/#pivot=sdk-tools)。 これらのパッケージは、基本的な Bot Builder SDK のクラスとメソッドを次のように拡張します。

* 365 コネクタ カードのような特殊なOfficeを使用します。
* アクティビティに対して Teams 固有のチャネル データを設定します。
* メッセージング拡張要求を処理する。

> [!IMPORTANT]
> 任意の Web プログラミング テクノロジで Teams アプリを開発し [、Bot Framework REST API を直接呼び出](/bot-framework/rest-api/bot-framework-rest-overview) します。 ただし、すべてのケースでトークン処理を実行する必要があります。

> [!TIP]
> Teams App Studio を使用すると、アプリ マニフェストを作成および構成し、ボット フレームワークにボットとして Web サービスを登録できます。 また、React 制御ライブラリと、対話型カードのビルダーも用意されています。 詳細については [、「Teams App Studio の使用を開始する」を参照してください](~/concepts/build-and-test/app-studio-overview.md)。

## <a name="bots-and-the-microsoft-power-virtual-agents"></a>ボットと Microsoft Power 仮想エージェント

[Power Virtual Agents は](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) 、Microsoft Power プラットフォームと Bot Framework 上に構築されたチャットボット サービスです。 Power Virtual Agent 開発プロセスでは、ガイド付き、コードなし、グラフィカル インターフェイスのアプローチを使用して、チーム メンバーがインテリジェントな仮想エージェントを簡単に作成および維持できます。 Power Virtual Agents ポータルでチャットボットを作成した後 [、Teams](https://powervirtualagents.microsoft.com)と簡単 [に統合できます](how-to/add-power-virtual-agents-bot-to-teams.md)。 開始方法の詳細については [、「Power Virtual Agents」のドキュメントを参照してください](https://docs.microsoft.com/power-virtual-agents/)。

## <a name="bots-and-webhooks-and-connectors"></a>ボットと Webhooks とコネクタ

Webhooks とコネクタは、ボットを Web サービスに接続します。 Webhooks とコネクタを使用すると、ワークフローや他の簡単なコマンドの作成など、基本的な操作を行う簡単なボットを作成できます。 これらは、作成したチームでのみ使用できます。会社のワークフローに固有の単純なプロセスを対象とします。 詳細については [、「webhooks とコネクタについて」を参照してください](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)。

## <a name="advantages-of-bots"></a>ボットの利点

Microsoft Teams のボットは、1 対 1 の会話、グループ チャット、チーム内のチャネルで扱うことができます。 各スコープは、会話ボットに固有の機会と課題を提供します。

| チャネル | グループ チャット | 1 対 1 のチャット |
| :-- | :-- | :-- |
| 大規模なリーチ | メンバーの数が少ない | 従来の方法 |
| 個々の対話を簡潔に | @mentionボットへのアクセス  | Q&ボット |
| @mentionボットへのアクセス | チャネルに似ている | ジョークを伝え、メモを取るボット |

### <a name="in-a-channel"></a>チャネル

チャネルには、最大 2,000 人までの複数のユーザー間のスレッド会話が含まれる。 これにより、ボットに大量のリーチが生まれる可能性がありますが、個々のやり取りは簡潔である必要があります。 従来のマルチターン操作は機能しません。 代わりに、対話型カードまたはタスク モジュールを使用するか、会話を 1 対 1 の会話に移動して多くの情報を収集する必要があります。 ボットにはメッセージへのアクセスのみ許可されます `@mentioned` 。 Microsoft Graph と組織レベルのアクセス許可を使用して、会話から追加のメッセージを取得できます。

ボットは、次の場合にチャネルで優れた機能を提供します。

* 通知: ユーザーが追加情報を取得する対話型カードを提供します。
* アンケートやアンケートなどのフィードバック シナリオ。
* 単一の要求または応答サイクルは対話を解決し、結果は会話の複数のメンバーに役立ちます。
* ソーシャルボットや楽しいボット。素晴らしい猫の画像を取得し、ランダムに勝者を選ぶなどです。

### <a name="in-a-group-chat"></a>グループ チャット

グループ チャットは、3 人以上のユーザー同士で行われる非スレッドの会話です。 チャネルよりもメンバーは少なく、一時的な会話が多いのが特徴です。 チャネルと同様に、ボットはメッセージに直接アクセスできる `@mentioned` のみです。

チャネルでボットがうまく機能する場合は、グループ チャットの方がうまく機能します。

### <a name="in-a-one-to-one-chat"></a>1 対 1 のチャット

1 対 1 のチャットは、会話ボットがユーザーと対話する従来の方法です。 1 対 1 の会話型ボットの例としては、Q&ボット、他のシステムでワークフローを開始するボット、ジョークを伝えるボット、メモを取るボットがあります。 1 対 1 のチャットボットを作成する前に、会話ベースのインターフェイスが機能を提示する最適な方法であるかどうかを検討してください。

## <a name="disadvantages-of-bots"></a>ボットの欠点

ボットとユーザーの間の広範なダイアログは、タスクを完了するための低速で複雑な方法です。 過剰なコマンド、特に広範なコマンドをサポートするボットは、ユーザーが成功または肯定的に表示されません。

### <a name="have-multi-turn-experiences-in-chat"></a>チャットでのマルチターン エクスペリエンス

広範なダイアログでは、開発者が状態を維持する必要があります。 この状態を終了するには、ユーザーがタイム アウトするか、[キャンセル] を選択する **必要があります**。 また、このプロセスは時間のかかっています。 たとえば、次の会話シナリオを参照してください。

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

## <a name="code-sample"></a>コード サンプル

|サンプルの名前 | 説明 | .NETCore | Node.js |
|----------------|-----------------|--------------|----------------|
| Teams 会話ボット | メッセージングおよび会話イベントの処理。 |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot)|

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [ボットのアクティビティ ハンドラー](~/bots/bot-basics.md)
