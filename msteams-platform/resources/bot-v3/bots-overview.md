---
title: Microsoft Teams アプリにボットを追加する
description: Microsoft Teams でボットの開発を開始する方法について説明します。
ms.topic: conceptual
keywords: チーム ボットの開発
ms.date: 05/20/2018
ms.openlocfilehash: 226340500f59754d603f21b7868eecab38f942af
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014405"
---
# <a name="add-bots-to-microsoft-teams-apps"></a>Microsoft Teams アプリにボットを追加する

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

インテリジェントなボットを構築して接続し、チャットを通じて Microsoft Teams ユーザーと自然に対話します。 または、より広範な Teams アプリ エクスペリエンスのための "コマンド ライン" インターフェイスとして使用する、単純なコマンド ベースのボットを提供します。 通知専用ボットを作成して、ユーザーに関連する情報をチャネルや直接メッセージで直接ユーザーにプッシュできます。 既存の Bot Framework ベースのボットを持ち込み、Teams 固有のサポートを追加してエクスペリエンスを向上させる方法も可能です。

![ユーザーを支援するボットの例](~/assets/images/bot_example.png)

## <a name="what-you-need-to-know-bots"></a>知る必要がある情報: ボット

ボットは、会話で対話する他のチーム メンバーと同じ方法で表示されます。ただし、ボットにはアバターアイコンが付き、常にオンラインです。

ボットの動作は、関係する会話の種類によって異なります。 Teams のボットは、いくつかの種類の会話 (アプリ マニフェストではスコープと呼ばれる) [をサポートしています](~/resources/schema/manifest-schema.md)。

* `teams` チャネル会話とも呼ばれる
* `personal` ボットと 1 人のユーザーの会話
* `groupChat` ボットと 2 人以上のユーザーの会話

詳細 [については、「Microsoft Teams ボットと会話する](~/resources/bot-v3/bot-conversations/bots-conversations.md) 」を参照してください。

Microsoft Teams アプリを使用すると、ボットをエクスペリエンスのスターにしたり、単にヘルパーにすることもできます。 ボットは、タブやメッセージング拡張機能などの他の機能を含む広範なアプリ パッケージの[](~/tabs/what-are-tabs.md)一部[として配布されます](~/messaging-extensions/what-are-messaging-extensions.md)。

## <a name="bot-apis"></a>Bot API

Microsoft Teams は [、Microsoft Bot Framework のほとんどをサポートしています](https://dev.botframework.com/)。 (Bot Framework に基づくボットが既にある場合は、そのボットを Microsoft Teams での動作に容易に適応させることができます)。[SDK](/microsoftteams/platform/#pivot=sdk-tools) を利用するには、C# か Node.js のどちらかを使用することをお勧めします。 これらのパッケージは、以下の基本的な Bot Builder SDK のクラスとメソッドを拡張します。

* Office 365 コネクタ カードのような特殊なカードの種類を使用する
* アクティビティに関する Teams 固有のチャネル データの使用と設定
* メッセージング拡張機能要求の処理

SDK 拡張機能は、Bot Builder SDK を含む依存関係をインストールします。

* **.NET** Bot Builder SDK for .NET の Microsoft Teams 拡張機能を使用するには [、Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet パッケージを Visual Studioします。 開発Node.js、Microsoft Teams の BotBuilder 機能は、v4.6 の現在 [Bot Framework SDK](https://github.com/microsoft/botframework-sdk) に組み込まれています。

*Bot* Framework の [サンプルも参照してください](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。

> [!IMPORTANT]
> 他の任意の Web プログラミング テクノロジで Teams アプリを開発し [、Bot Framework REST](/bot-framework/rest-api/bot-framework-rest-overview) API を直接呼び出しますが、すべてのトークン処理を自分で実行する必要があります。

*Teams App Studio は* 、アプリ マニフェストの作成と構成に役立ち、Bot Framework ボットを作成するのに役立ちます。 また、React 制御ライブラリと、対話型カードのビルダーも用意されています。

## <a name="outgoing-webhooks"></a>送信 Webhook

送信 Webhook を使用すると、ワークフローの開始や必要な他の簡単なコマンドなど、基本的な操作のための単純なボットを作成できます。 送信 Webhook は、作成したチーム内でのみ使用され、会社のワークフローに固有の単純なプロセスを対象とします。 詳細 [については、送信 Webhook を](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md) 参照してください。

## <a name="build-a-great-teams-bot"></a>Teams のボットを作成する

次のトピックでは、Teams 用に最適なボットを作成するプロセスについて説明します。

* [ボットを作成](~/resources/bot-v3/bots-create.md)する : Bot Framework チームが提供する、便利なツール、ドキュメント、コミュニティを活用します。
* [ボットと話す](~/resources/bot-v3/bot-conversations/bots-conversations.md): 基本的な会話フローを追加し、チャネル固有の機能を活用します。 .NET または Node.js で開発する場合は、Bot Builder SDK の拡張機能を使用して作業を簡素化します。
* [ボットでのカードの使用](~/resources/bot-v3/bots-cards.md) ユーザーの応答を伝え、受け入れるカードを設計します。
* [ボット イベントに応答します](~/resources/bot-v3/bots-notifications.md)。
* [通知専用ボット](~/resources/bot-v3/bots-notification-only.md) ボットを使用してアプリの通知を送信する。
* [コンテキストを取得する](~/resources/bot-v3/bots-context.md) ユーザーに関する情報を取得します。
* [ボット メニュー](~/resources/bot-v3/bots-menus.md) ボットでのメニューの使用。
* [ボットとファイル](~/resources/bot-v3/bots-files.md) ボットからのファイルの送受信。
* [ボットでタブを使用する](~/resources/bot-v3/bots-with-tabs.md) タブとボットを組み合わせて使用する。
* [ボットをテスト](~/resources/bot-v3/bots-test.md)する: ボットを追加して、個人またはチームの会話を行い、動作を確認します。
