---
title: 話し言葉の bot とは
author: clearab
description: Microsoft Teams の会話ボットの概要。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 7bde886b67788a355181c83287d999a3bfb9727a
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674746"
---
# <a name="what-are-conversational-bots"></a>話し言葉の bot とは

話し言葉の bot は、ユーザーがテキスト、インタラクティブなカード、およびタスクモジュールを使用して web サービスと対話できるようにします。 これらは非常に柔軟になっており、話し言葉の bot は、いくつかの簡単なコマンドや、複雑で人為的な知性を備えた、自然言語処理仮想アシスタントを処理するようにスコープを設定できます。 これは、大規模なアプリケーションの1つの側面、または完全に独立したものにすることができます。

次の GIF は、テキストカードとインタラクティブカードの両方を使用して、1対1のチャットに bot があるユーザー conversing を示しています。 カード、テキスト、タスクモジュールを適切に組み合わせて見つけることは、便利な bot を作成するための鍵となります。 忘れずに、ボットはテキストだけではありません。

![FAQ + gif](~/assets/images/FAQPlusEndUser.gif)

## <a name="what-tasks-are-best-handled-by-bots"></a>Bot が最適に処理できるタスク

Microsoft Teams のボットは、1対1の会話、グループチャット、またはチーム内のチャネルの一部にすることができます。 各スコープによって、会話の bot に固有の機会と課題が提供されます。

### <a name="in-a-channel"></a>チャネル内

チャネルには、複数のユーザー間のスレッド化された会話が含まれています。多くのユーザー (現在は最大 2000)。 これにより、ボットが大規模になる可能性がありますが、個々の相互作用を簡潔にする必要があります。 従来のマルチターンの対話は、おそらくうまく機能しません。 その代わりに、多くの情報を収集する必要がある場合は、対話形式のカードまたはタスクモジュールを使用するか、会話を1対1の会話に移動することをお探しください。 Bot は、直接メッセージにアクセスできるだけで、Microsoft `@mentioned` Graph を使用して会話から他のメッセージを取得することも、組織レベルの管理者レベルのアクセス許可を使用することもできません。

チャネルのボット excel には、次のようなシナリオがあります。

* **通知**(特に、ユーザーが追加情報を必要とする対話カードを提供している場合)。
* 投票や調査などの**フィードバックシナリオ**。
* **単一の要求/応答サイクル**で解決できる相互作用。これにより、結果は会話の複数のメンバーにとって役に立ちます。
* **ソーシャル/おもしろいボット**—すばらしい cat 画像を取得し、ランダムに選択します。

### <a name="in-a-group-chat"></a>グループチャット

グループチャットは、3人以上のユーザー間のスレッド以外の会話です。 チャネルのメンバー数が少なくなる傾向があります。 チャネルに似ていますが、bot は`@mentioned`直接メッセージにアクセスできます。

通常、チャネルで正常に動作するシナリオは、グループチャットでも同様に機能します。

### <a name="in-a-one-to-one-chat"></a>ワンツーワンチャット

これは、会話の bot がユーザーと対話するための従来の方法です。 これにより、非常に多様なワークロードを実現できます。 Q&他のシステムでワークフローを開始する bot、ジョークになる bot、およびメモを取る bot は、いくつかの例にすぎません。 会話ベースのインターフェイスが機能を提供するのに最適な方法かどうかを考慮することを忘れないでください。

## <a name="how-do-bots-work"></a>Bot はどのように動作しますか?

Bot は3つの部分で構成されます。

* ホストしているパブリックアクセス可能な web サービス。
* Bot を Bot フレームワークに登録する bot 登録。
* アプリマニフェストを含む Teams アプリパッケージ。 これは、ユーザーがインストールし、Teams クライアントを web サービス (Bot サービスを経由してルーティング) に接続することです。

Microsoft Teams のボットは、 [Microsoft Bot フレームワーク](https://dev.botframework.com/)に基づいて構築されています。 (Bot フレームワークに基づく bot が既にある場合は、それを Microsoft Teams での動作に容易に適応させることができます)。[Sdk](/microsoftteams/platform/#pivot=sdk-tools)を利用するには、C# または node.js のどちらかを使用することをお勧めします。 これらのパッケージは、基本的な Bot ビルダー SDK のクラスとメソッドを拡張します。

* Office 365 コネクタカードなどの特殊なカードの種類を使用します。
* アクティビティのチーム固有のチャネルデータの使用と設定。
* メッセージング拡張要求を処理する。

> [!IMPORTANT]
> 任意の web プログラミングテクノロジで Teams アプリを開発し、 [Bot フレームワーク REST api](/bot-framework/rest-api/bot-framework-rest-overview)を直接呼び出すことができますが、すべてのトークン処理を自分自身で実行する必要があります。

*Teams アプリ Studio*は、アプリマニフェストを作成して構成し、web サービスを bot フレームワーク上の bot として登録できます。 また、コントロールライブラリとインタラクティブカードビルダーを備えています。 「 [Teams アプリ Studio の](~/concepts/build-and-test/app-studio-overview.md)概要 *」を参照してください*。

## <a name="webhooks-and-connectors"></a>Webhooks とコネクタ

Webhooks とコネクタを使用すると、ワークフローまたは他の単純なコマンドのや議など、基本的な操作のための簡単な bot を作成できます。 これらのユーザーは、それらを作成したチーム内にのみ存在し、会社のワークフローに固有の単純なプロセスを対象としています。 詳細について[は、「webhook とコネクタ](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)につい*て」を参照して*ください。

## <a name="get-started"></a>作業の開始

* [C#/dotnet での Teams 会話のボット](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot)
* [JavaScript での Teams の会話のボット](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot)

## <a name="learn-more"></a>詳細情報

* [Teams でのボットの基本](~/bots/bot-basics.md)
* [Teams の bot を作成する](~/bots/how-to/create-a-bot-for-teams.md)
