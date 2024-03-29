---
title: Microsoft Teams アプリにボットを追加する
description: このモジュールでは、Microsoft Teams でボットの開発を開始する方法と、Teams でボットを追加するためのすべての要件について説明します
ms.topic: conceptual
ms.localizationpriority: medium
ms.date: 05/20/2018
ms.openlocfilehash: a1563d72ada21810393d7a0118b5a2b94463a27b
ms.sourcegitcommit: 69a45722c5c09477bbff3ba1520e6c81d2d2d997
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/11/2022
ms.locfileid: "67312213"
---
# <a name="add-bots-to-microsoft-teams-apps"></a>Microsoft Teams アプリにボットを追加する

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

インテリジェント ボットを構築して接続し、チャットを通じて自然に Microsoft Teams ユーザーと対話します。 または、より広範な Teams アプリ エクスペリエンスの "コマンド ライン" インターフェイスとして使用する、単純なコマンド ベースのボットを提供します。 通知専用ボットを作成すると、ユーザーに関連する情報をチャネルまたはダイレクト メッセージで直接プッシュできます。 既存の Bot Framework ベースのボットを導入し、Teams 固有のサポートを追加して、エクスペリエンスを輝かせます。

> [!IMPORTANT]
> 現在、ボットは Government Community Cloud (GCC) とGCC-Highで利用できますが、国防総省 (DOD) では利用できません。

:::image type="content" source="../../assets/images/bot_example.png" alt-text="ユーザーを支援するボットの例":::

## <a name="what-you-need-to-know-bots"></a>知っておく必要がある情報: ボット

ボットは、会話でやり取りする他のチーム メンバーと同じように表示されます。ただし、ボットには六角形のアバター アイコンがあり、常にオンラインです。

ボットの動作は、ボットが関係する会話の種類によって異なります。 Teams のボットでは、[アプリ マニフェスト](~/resources/schema/manifest-schema.md)のスコープと呼ばれるいくつかの種類の会話がサポートされています。

* `teams` チャネル会話とも呼ばれます。
* `personal` ボットと 1 人のユーザーとの会話。
* `groupChat` ボットと 2 人以上のユーザー間の会話。

詳細については、「[Microsoft Teams ボットと会話する](~/resources/bot-v3/bot-conversations/bots-conversations.md)」を参照してください。

Teams アプリを使用すると、ボットをエクスペリエンスのスターにすることも、ヘルパーにすることもできます。 ボットは、 [タブ](~/tabs/what-are-tabs.md) や [メッセージ拡張機能](~/messaging-extensions/what-are-messaging-extensions.md)などの他の機能を含めることができる広範なアプリ パッケージの一部として配布されます。

## <a name="bot-apis"></a>ボット API

Teams では、ほとんどのMicrosoft Bot Frameworkがサポート[されています](https://dev.botframework.com/)。 (Bot Framework に基づくボットが既にある場合は、Teams で動作するように簡単に調整できます)。SDK を利用するには、C# またはNode.jsのいずれかを使用することをお勧[めします。](/microsoftteams/platform/#pivot=sdk-tools) これらのパッケージは、以下の基本的な Bot Builder SDK のクラスとメソッドを拡張します。

* Office 365 コネクタ カードなどの専用のカードの使用。
* アクティビティに関する Teams 固有のチャネル データの使用と設定。
* メッセージング拡張要求の処理。

SDK 拡張機能は、ボット ビルダー SDK を含む依存関係をインストールします。

* **.NET** .NET のボット ビルダー SDK 用の Microsoft Teams 拡張機能を使用するには、Visual Studio プロジェクトに [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet パッケージをインストールします。 Node.js 開発では、Microsoft Teams 機能用のボット ビルダーが v4.6 の時点で [Bot Framework SDK](https://github.com/microsoft/botframework-sdk) に組み込まれています。

> [!IMPORTANT]
> 任意の Web プログラミング技術で Teams アプリを開発し、[Bot Framework REST API](/bot-framework/rest-api/bot-framework-rest-overview) を直接呼び出すことができますが、すべてのトークン処理を自分で実行する必要があります。

*Teams 用開発者ポータル* は、アプリ マニフェストの作成と構成に役立ち、Bot Framework ボットを作成できます。 また、React 制御ライブラリと、対話型カードのビルダーも用意されています。

## <a name="outgoing-webhooks"></a>送信 Webhook

送信 Webhook を使用すると、ワークフローやその他の必要な単純なコマンドの開始など、基本的な操作のための単純なボットを作成できます。 送信 Webhook は、それを作成したチームにのみ存在し、会社のワークフローに固有の単純なプロセスを対象としています。 詳細については、「[送信 Webhook](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)」を参照してください。

## <a name="build-a-great-teams-bot"></a>優れたTeams ボットをビルドする

次の記事では、Teams 用の優れたボットを作成するプロセスについて説明します。

* [ボットを作成する](~/resources/bot-v3/bots-create.md): Bot Framework チームが提供する優れたツール、ドキュメント、コミュニティを活用します。
* [ボットと会話する](~/resources/bot-v3/bot-conversations/bots-conversations.md): 基本的な会話フローを追加し、チャネル固有の機能を活用します。 .NET または Node.js で開発する場合は、ボット ビルダー SDK の拡張機能を使用して作業を簡略化します。
* [ボットでカードを使用する](~/resources/bot-v3/bots-cards.md): カードを設計して、ユーザーの応答を通信して受け入れます。
* [ボット イベントに応答する](~/resources/bot-v3/bots-notifications.md)
* [通知のみのボット](~/resources/bot-v3/bots-notification-only.md): ボットを使用して、アプリの通知を送信します。
* [コンテキストの取得](~/resources/bot-v3/bots-context.md): 現在のユーザーの情報を取得します。
* [ボット メニュー](~/resources/bot-v3/bots-menus.md): ボットでメニューを使用する。
* [ボットとファイル](~/resources/bot-v3/bots-files.md): ボットからのファイルの送受信。
* [ボットでタブを使用する](~/resources/bot-v3/bots-with-tabs.md): タブとボットを連携させる。
* [ボットをテスト](~/resources/bot-v3/bots-test.md)する: 個人用またはチームの会話用にボットを追加して、ボットが動作しているのを確認します。

## <a name="see-also"></a>関連項目

[Bot Framework サンプル](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。
