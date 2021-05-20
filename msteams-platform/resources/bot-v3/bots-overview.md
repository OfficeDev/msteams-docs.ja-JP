---
title: Microsoft Teamsアプリにボットを追加する
description: Microsoft Teamsでボットの開発を開始する方法について説明します。
ms.topic: conceptual
keywords: チームボット開発
localization_priority: Normal
ms.date: 05/20/2018
ms.openlocfilehash: 674576efccb2916b8a82ae27310d8fe49909a782
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566755"
---
# <a name="add-bots-to-microsoft-teams-apps"></a>Microsoft Teamsアプリにボットを追加する

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

インテリジェントボットを構築し、チャットを通じて自然にMicrosoft Teamsユーザーと対話するように接続します。 または、より幅広いTeamsアプリエクスペリエンスのための「コマンドライン」インターフェイスとして使用する、単純なコマンドベースのボットを提供します。 通知専用のボットを作成すると、チャンネルまたはダイレクトメッセージでユーザーに関連する情報を直接ユーザーにプッシュできます。 既存の Bot Framework ベースのボットを利用して、Teams固有のサポートを追加して、エクスペリエンスを高めることができます。

![ユーザーを支援するボットの例](~/assets/images/bot_example.png)

## <a name="what-you-need-to-know-bots"></a>知っておくべきこと: ボット

ボットは、会話でやり取りする他のチーム メンバーと同じように表示されます。

ボットは、どのような会話に関係するかによって動作が異なります。 Teamsのボットは、[アプリ マニフェスト](~/resources/schema/manifest-schema.md)のスコープと呼ばれるいくつかの種類の会話をサポートしています。

* `teams` チャネル会話とも呼ばれます。
* `personal` ボットと単一ユーザーの会話。
* `groupChat` ボットと 2 人以上のユーザーの間の会話。

詳細については、「 [Microsoft Teams ボットとの会話 」](~/resources/bot-v3/bot-conversations/bots-conversations.md)を参照してください。

Microsoft Teamsアプリを使用すると、ボットをエクスペリエンスのスターにしたり、単なるヘルパーにすることができます。 ボットは、 [タブ](~/tabs/what-are-tabs.md) や [メッセージング拡張機能](~/messaging-extensions/what-are-messaging-extensions.md)などの他の機能を含むことができる、より広範なアプリ パッケージの一部として配布されます。

## <a name="bot-apis"></a>ボット API

Microsoft Teams[は、ほとんどのMicrosoft Bot Framework](https://dev.botframework.com/)をサポートしています。 (Bot Framework に基づくボットが既にある場合は、そのボットを Microsoft Teams での動作に容易に適応させることができます)。[SDK](/microsoftteams/platform/#pivot=sdk-tools) を利用するには、C# か Node.js のどちらかを使用することをお勧めします。 これらのパッケージは、以下の基本的な Bot Builder SDK のクラスとメソッドを拡張します。

* Office 365 コネクタ カードなどの専用のカードの使用。
* アクティビティに関する Teams 固有のチャネル データの使用と設定。
* メッセージング拡張要求の処理。

SDK 拡張機能は、ボット ビルダー SDK を含む依存関係をインストールします。

* **NET** ボット ビルダー SDK for .NET のMicrosoft Teams拡張機能を使用するには、Visual Studio プロジェクトに [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet パッケージをインストールします。 Node.js開発のために、ボットビルダーのMicrosoft Teams機能は v4.6 の[時点でボット フレームワーク SDK](https://github.com/microsoft/botframework-sdk)に組み込まれています。

> [!IMPORTANT]
> 他の Web プログラミング テクノロジでTeamsアプリを開発し[、Bot Framework REST API を](/bot-framework/rest-api/bot-framework-rest-overview)直接呼び出すことができますが、すべてのトークン処理を自分で実行する必要があります。

*Teamsアプリスタジオ* では、アプリ マニフェストの作成と構成を行い、ボット フレームワーク ボットを作成できます。 また、React 制御ライブラリと、対話型カードのビルダーも用意されています。

## <a name="outgoing-webhooks"></a>送信 Webhook

送信 webhook を使用すると、ワークフローや必要なその他の簡単なコマンドを開始するなどの基本的な操作のための単純なボットを作成できます。 送信 webhook は、ユーザーが作成したチーム内にのみ存続し、会社のワークフローに固有の単純なプロセスを対象としています。 詳細については、発信 [webhook を](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)参照してください。

## <a name="build-a-great-teams-bot"></a>優れたTeamsボットを構築する

次のトピックでは、Teamsに最適なボットを作成するプロセスについて説明します。

* [ボットの作成](~/resources/bot-v3/bots-create.md): Bot Framework チームが提供する優れたツール、ドキュメント、コミュニティを活用します。
* [ボットに話す](~/resources/bot-v3/bot-conversations/bots-conversations.md): 基本的な会話フローを追加し、チャネル固有の機能を活用します。 NET または Node.js で開発する場合は、Bot Builder SDK の拡張機能を使用して作業を簡略化します。
* [ボットでカードを使用](~/resources/bot-v3/bots-cards.md)する : カードをデザインして通信し、ユーザーの応答を受け入れます。
* [ボット イベントに応答する](~/resources/bot-v3/bots-notifications.md)
* [通知専用ボット](~/resources/bot-v3/bots-notification-only.md): ボットを使用してアプリの通知を送信します。
* [コンテキストの取得](~/resources/bot-v3/bots-context.md): ユーザーに関する情報を取得します。
* [ボットメニュー](~/resources/bot-v3/bots-menus.md): ボットでメニューを使用する。
* [ボットとファイル](~/resources/bot-v3/bots-files.md): ボットからファイルを送受信します。
* [ボットでタブを使用](~/resources/bot-v3/bots-with-tabs.md)する : タブとボットを連携させる。
* [ボットをテストする](~/resources/bot-v3/bots-test.md): ボットを追加して、個人やチームでの会話を行って、実際に見ることができます。

## <a name="see-also"></a>関連項目

[ボット フレームワークのサンプル](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)