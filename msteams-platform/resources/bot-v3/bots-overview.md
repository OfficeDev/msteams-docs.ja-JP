---
title: Microsoft Teams アプリにボットを追加する
description: Microsoft Teams でボットの開発を始める方法について説明します。
keywords: teams のボット開発
ms.date: 05/20/2018
ms.openlocfilehash: 58221e94520ef6e748bbd6c17fa7933813874c56
ms.sourcegitcommit: 6c5c0574228310f844c81df0d57f11e2037e90c8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2020
ms.locfileid: "42228053"
---
# <a name="add-bots-to-microsoft-teams-apps"></a>Microsoft Teams アプリにボットを追加する

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

チャットを通じて Microsoft Teams ユーザーと対話するためのインテリジェントボットを構築して接続します。 または、より幅広い Teams アプリ環境の "コマンドライン" インターフェイスとして使用するために、簡単なコマンドベースのボットを提供します。 通知専用ボットを作成して、ユーザーに関連する情報をチャネルまたは直接メッセージに直接プッシュすることができます。 既存の Bot フレームワークを使用している bot を利用して、チーム固有のサポートを追加して、快適にご利用いただけるようにすることもできます。

![ユーザーを支援する bot の例](~/assets/images/bot_example.png)

## <a name="what-you-need-to-know-bots"></a>知っておくべきこと: Bot

Bot は、会話でやりとりする他のチームメンバーと同じように表示されます。ただし、六角アイコンがあり、常にオンラインになっています。

Bot の動作は、関係する会話の種類によって異なります。 Teams の bot は、いくつかの種類の会話 ([アプリマニフェスト](~/resources/schema/manifest-schema.md)でのスコープと呼ばれます) をサポートしています。

* `teams`チャネル会話とも呼ばれます。
* `personal`Bot と1人のユーザーとの会話
* `groupChat`ボットと2人以上のユーザー間の会話

詳細については[、「Microsoft Teams の bot との会話](~/resources/bot-v3/bot-conversations/bots-conversations.md)」を参照してください。

Microsoft Teams アプリを使用すると、ボットを星で使用したり、ヘルパーとしたりすることができます。 Bot は、[タブ](~/tabs/what-are-tabs.md)や[メッセージング拡張](~/messaging-extensions/what-are-messaging-extensions.md)機能などの他の機能を含む、幅広いアプリパッケージの一部として配布されます。

## <a name="bot-apis"></a>Bot Api

Microsoft Teams は、 [Microsoft Bot フレームワーク](https://dev.botframework.com/)の大部分をサポートしています。 (Bot フレームワークに基づく bot が既にある場合は、それを Microsoft Teams での動作に容易に適応させることができます)。[Sdk](/microsoftteams/platform/#pivot=sdk-tools)を利用するには、C# または node.js のどちらかを使用することをお勧めします。 これらのパッケージは、基本的な Bot ビルダー SDK のクラスとメソッドを拡張します。

* Office 365 コネクタカードなどの専用カードの種類を使用する
* アクティビティでのチーム固有のチャネルデータの使用と設定
* メッセージング拡張要求の処理

SDK 拡張機能は、Bot ビルダー SDK を含む依存関係をインストールします。

* **.Net**Bot ビルダー SDK for .NET の Microsoft Teams 拡張機能を使用するには、Visual Studio プロジェクトに、 [teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet パッケージをインストールします。 Node.js の開発では、Microsoft Teams の BotBuilder の機能が、v2.0 [FRAMEWORK SDK](https://github.com/microsoft/botframework-sdk) in v2.0 に組み込まれています。

[Bot フレームワークサンプル](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)*も参照してください*。

> [!IMPORTANT]
> 他の web プログラミングテクノロジで Teams アプリを開発し、 [Bot フレームワーク REST api](/bot-framework/rest-api/bot-framework-rest-overview)を直接呼び出すことができますが、すべてのトークン処理を自分自身で実行する必要があります。

*Teams App Studio*は、アプリのマニフェストを作成および構成するのに役立つので、bot フレームワーク bot を作成できます。 また、コントロールライブラリとインタラクティブカードビルダーを備えています。

## <a name="outgoing-webhooks"></a>送信 web フック

送信用の webhook を使用すると、基本的な操作のための簡単な bot を作成できます。たとえば、ワークフローや、必要に応じた他の単純なコマンドのや議などです。 送信 web フックは、それらを作成したチーム内のみで、会社のワークフローに固有の単純なプロセスを対象としています。 詳細については、「[送信 webhook](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md) 」を参照してください。

## <a name="build-a-great-teams-bot"></a>Teams bot を構築する

次のトピックでは、Teams の大 bot を作成するプロセスについて説明します。

* [Bot を作成する](~/resources/bot-v3/bots-create.md): bot フレームワークチームによって提供される優れたツール、ドキュメント、コミュニティを活用してください。
* [Bot に連絡して、](~/resources/bot-v3/bot-conversations/bots-conversations.md)基本的な会話フローを追加し、チャネル固有の機能を利用します。 .NET または node.js で開発する場合は、ボット Builder SDK の拡張機能を使用して作業を簡略化します。
* [Bot でのカードの使用](~/resources/bot-v3/bots-cards.md)デザインカードを使用して、ユーザーの応答をやり取りします。
* [Bot イベントに応答](~/resources/bot-v3/bots-notifications.md)します。
* [通知専用ボット](~/resources/bot-v3/bots-notification-only.md)ボットを使用してアプリの通知を送信します。
* [コンテキストを取得](~/resources/bot-v3/bots-context.md)するユーザーに関する情報を取得します。
* [Bot メニュー](~/resources/bot-v3/bots-menus.md)Bot でメニューを使用します。
* [ボットとファイル](~/resources/bot-v3/bots-files.md)ボットからファイルを送受信する。
* [Bot でタブを使用する](~/resources/bot-v3/bots-with-tabs.md)タブと bot を連携させる。
* [Bot をテスト](~/resources/bot-v3/bots-test.md)します。個人またはチームの会話に bot を追加して、動作を確認します。
