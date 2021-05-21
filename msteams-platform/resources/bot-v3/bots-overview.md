---
title: ボットを他のアプリMicrosoft Teamsする
description: ボットの開発を開始する方法について説明Microsoft Teams
ms.topic: conceptual
keywords: teams ボットの開発
localization_priority: Normal
ms.date: 05/20/2018
ms.openlocfilehash: 674576efccb2916b8a82ae27310d8fe49909a782
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566755"
---
# <a name="add-bots-to-microsoft-teams-apps"></a>ボットを他のアプリMicrosoft Teamsする

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

インテリジェント ボットを構築して接続し、チャットを通Microsoft Teamsユーザーと対話します。 または、簡単なコマンド ベースのボットを提供して、より広範なアプリ エクスペリエンスを提供する "コマンドライン" インターフェイスTeams提供します。 通知専用ボットを作成して、ユーザーに関連する情報をチャネルまたはダイレクト メッセージで直接プッシュできます。 既存の Bot Framework ベースのボットを持ち込み、Teams固有のサポートを追加して、エクスペリエンスを向上させる方法も可能です。

![ユーザーを支援するボットの例](~/assets/images/bot_example.png)

## <a name="what-you-need-to-know-bots"></a>知る必要があるもの: ボット

ボットは、会話で操作する他のチーム メンバーと同様に表示されます。ただし、ボットは六角形のアバター アイコンを持ち、常にオンラインです。

ボットの動作は、関係する会話の種類に応じて異なります。 ボットはTeamsマニフェストのスコープと呼ばれるいくつかの種類の会話を[サポートします](~/resources/schema/manifest-schema.md)。

* `teams` チャネルの会話とも呼ばれる。
* `personal` ボットと 1 人のユーザーの会話。
* `groupChat` ボットと 2 人以上のユーザーとの会話。

詳細については、「チャット ボットと会話する[」をMicrosoft Teamsしてください](~/resources/bot-v3/bot-conversations/bots-conversations.md)。

アプリMicrosoft Teams、ボットをエクスペリエンスのスターにしたり、ヘルパーにすることもできます。 ボットは、タブやメッセージング拡張機能などの他の機能を含む、より広範なアプリ[](~/tabs/what-are-tabs.md)パッケージの一部[として配布されます](~/messaging-extensions/what-are-messaging-extensions.md)。

## <a name="bot-apis"></a>ボット API

Microsoft Teamsは、ほとんどの機能をサポート[Microsoft Bot Framework。](https://dev.botframework.com/) (Bot Framework に基づくボットが既にある場合は、そのボットを Microsoft Teams での動作に容易に適応させることができます)。[SDK](/microsoftteams/platform/#pivot=sdk-tools) を利用するには、C# か Node.js のどちらかを使用することをお勧めします。 これらのパッケージは、以下の基本的な Bot Builder SDK のクラスとメソッドを拡張します。

* Office 365 コネクタ カードなどの専用のカードの使用。
* アクティビティに関する Teams 固有のチャネル データの使用と設定。
* メッセージング拡張要求の処理。

SDK 拡張機能は、ボット ビルダー SDK を含む依存関係をインストールします。

* **.NET** ボット ビルダー SDK for .NET Microsoft Teams拡張機能を使用するには [、Microsoft.Bot.Connector.Teams NuGet](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)パッケージを Visual Studio プロジェクトにインストールします。 開発Node.js、v4.6 のMicrosoft Teamsボット フレームワーク[SDK](https://github.com/microsoft/botframework-sdk)に組み込まれています。

> [!IMPORTANT]
> 他の web プログラミング テクノロジTeamsアプリを開発し[、Bot Framework REST API](/bot-framework/rest-api/bot-framework-rest-overview)を直接呼び出できますが、すべてのトークン処理を自分で実行する必要があります。

*Teams App Studio を* 使用すると、アプリ マニフェストを作成および構成し、ボット フレームワーク ボットを作成できます。 また、React 制御ライブラリと、対話型カードのビルダーも用意されています。

## <a name="outgoing-webhooks"></a>送信 Webhook

送信 Webhook を使用すると、ワークフローのキックオフや必要なその他の簡単なコマンドなど、基本的な操作のための簡単なボットを作成できます。 送信 Webhook は、作成したチームにのみ適用され、会社のワークフローに固有の単純なプロセスを対象とします。 詳細については、「送信 [Webhooks」を参照してください](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)。

## <a name="build-a-great-teams-bot"></a>最適なボットをTeamsする

次のトピックでは、ユーザーに最適なボットを作成するプロセスをTeams。

* [ボットを作成する](~/resources/bot-v3/bots-create.md): Bot Framework チームが提供する素晴らしいツール、ドキュメント、コミュニティを活用します。
* [ボットに相談する](~/resources/bot-v3/bot-conversations/bots-conversations.md): 基本的な会話フローを追加し、チャネル固有の機能を活用します。 .NET またはユーザー設定で開発Node.js、ボット ビルダー SDK の拡張機能を使用して作業を簡略化します。
* [ボットでカードを使用する](~/resources/bot-v3/bots-cards.md): カードを設計して、ユーザーの応答を通信して受け入れる。
* [ボット イベントへの応答](~/resources/bot-v3/bots-notifications.md)
* [通知専用ボット](~/resources/bot-v3/bots-notification-only.md): ボットを使用してアプリの通知を送信します。
* [Get context](~/resources/bot-v3/bots-context.md): ユーザーに関する情報を取得します。
* [ボット メニュー](~/resources/bot-v3/bots-menus.md): ボットでメニューを使用する。
* [ボットとファイル](~/resources/bot-v3/bots-files.md): ボットからのファイルの送受信。
* [ボットでタブを使用する](~/resources/bot-v3/bots-with-tabs.md): タブとボットを一緒に動作します。
* [ボットをテストする](~/resources/bot-v3/bots-test.md): ボットを追加して、個人またはチームの会話を行い、そのボットを実際に確認します。

## <a name="see-also"></a>関連項目

[ボット フレームワークのサンプル](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。