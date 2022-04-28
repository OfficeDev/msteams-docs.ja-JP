---
title: Microsoft Teams アプリにボットを追加する
description: Microsoft Teamsでボットの開発を開始する方法について説明します
ms.topic: conceptual
keywords: teams bots 開発
ms.localizationpriority: medium
ms.date: 05/20/2018
ms.openlocfilehash: 164c8e518e38d506bbaf80f59edebfb18c07acec
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2022
ms.locfileid: "65103426"
---
# <a name="add-bots-to-microsoft-teams-apps"></a>Microsoft Teams アプリにボットを追加する

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

インテリジェント ボットを構築して接続し、チャットを通じて自然にMicrosoft Teamsユーザーと対話します。 または、より広範なTeamsアプリ エクスペリエンスの "コマンド ライン" インターフェイスとして使用する、単純なコマンド ベースのボットを提供します。 通知専用ボットを作成すると、ユーザーに関連する情報をチャネルまたはダイレクト メッセージで直接プッシュできます。 既存の Bot Framework ベースのボットを導入し、Teams固有のサポートを追加して、エクスペリエンスを輝かせます。

> [!IMPORTANT]
> 現在、ボットはGovernment Community Cloud (GCC) で利用できますが、GCC-Highおよび国防総省 (DOD) では利用できません。

![ユーザーを支援するボットの例](~/assets/images/bot_example.png)

## <a name="what-you-need-to-know-bots"></a>知っておくべきこと: ボット

ボットは、会話でやり取りする他のチーム メンバーと同じように表示されます。ただし、ボットには六角形のアバター アイコンがあり、常にオンラインです。

ボットの動作は、ボットが関係する会話の種類によって異なります。 Teamsのボットでは、[アプリ マニフェスト](~/resources/schema/manifest-schema.md)のスコープと呼ばれるいくつかの種類の会話がサポートされています。

* `teams` チャネル会話とも呼ばれます。
* `personal` ボットと 1 人のユーザー間の会話。
* `groupChat` ボットと 2 人以上のユーザー間の会話。

詳細については、「[Microsoft Teams ボットと会話する](~/resources/bot-v3/bot-conversations/bots-conversations.md)」を参照してください。

Microsoft Teams アプリを使用すると、ボットをエクスペリエンスのスターにすることも、ヘルパーにすることもできます。 ボットは、 [タブ](~/tabs/what-are-tabs.md) や [メッセージ拡張機能](~/messaging-extensions/what-are-messaging-extensions.md)などの他の機能を含めることができる広範なアプリ パッケージの一部として配布されます。

## <a name="bot-apis"></a>ボット API

Microsoft Teamsは、ほとんどのMicrosoft Bot Frameworkをサポート[しています](https://dev.botframework.com/)。 (Bot Framework に基づくボットが既にある場合は、そのボットを Microsoft Teams での動作に容易に適応させることができます)。[SDK](/microsoftteams/platform/#pivot=sdk-tools) を利用するには、C# か Node.js のどちらかを使用することをお勧めします。 これらのパッケージは、以下の基本的な Bot Builder SDK のクラスとメソッドを拡張します。

* Office 365 コネクタ カードなどの専用のカードの使用。
* アクティビティに関する Teams 固有のチャネル データの使用と設定。
* メッセージ拡張要求の処理。

SDK 拡張機能は、Bot Builder SDK を含む依存関係をインストールします。

* **.NET** Bot Builder SDK for .NET のMicrosoft Teams拡張機能を使用するには、Visual Studio プロジェクトに [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet パッケージをインストールします。 Node.js開発では、Microsoft Teams機能用の BotBuilder が v4.6 の時点で [Bot Framework SDK](https://github.com/microsoft/botframework-sdk) に組み込まれています。

> [!IMPORTANT]
> 他の Web プログラミング テクノロジでTeamsアプリを開発し、[Bot Framework REST API を](/bot-framework/rest-api/bot-framework-rest-overview)直接呼び出すことができますが、すべてのトークン処理を自分で実行する必要があります。

*Teams App Studio* を使用すると、アプリ マニフェストを作成および構成したり、Bot Framework ボットを作成したりできます。 また、React 制御ライブラリと、対話型カードのビルダーも用意されています。

## <a name="outgoing-webhooks"></a>送信 Webhook

送信 Webhook を使用すると、ワークフローや必要なその他の簡単なコマンドを開始するなどの基本的な操作用の単純なボットを作成できます。 送信 Webhook は、作成したチームにのみ存在し、会社のワークフローに固有の簡単なプロセスを対象としています。 詳細については、 [送信 Webhook に関するページを](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)参照してください。

## <a name="build-a-great-teams-bot"></a>優れたTeams ボットを構築する

次のトピックでは、Teams用の優れたボットを作成するプロセスについて説明します。

* [ボットを作成する: Bot](~/resources/bot-v3/bots-create.md) Framework チームが提供する優れたツール、ドキュメント、コミュニティを活用します。
* [ボットと会話する](~/resources/bot-v3/bot-conversations/bots-conversations.md): 基本的な会話フローを追加し、チャネル固有の機能を活用します。 .NET またはNode.jsで開発する場合は、Bot Builder SDK の拡張機能を使用して作業を簡略化します。
* [ボットでカードを使用する](~/resources/bot-v3/bots-cards.md): カードを設計して、ユーザーの応答を通信して受け入れます。
* [ボット イベントに応答する](~/resources/bot-v3/bots-notifications.md)
* [通知専用ボット](~/resources/bot-v3/bots-notification-only.md): ボットを使用してアプリの通知を送信します。
* [コンテキストを取得](~/resources/bot-v3/bots-context.md)する: ユーザーに関する情報を取得します。
* [ボット メニュー](~/resources/bot-v3/bots-menus.md): ボットでメニューを使用する。
* [ボットとファイル](~/resources/bot-v3/bots-files.md): ボットからのファイルの送受信。
* [ボットでタブを使用する](~/resources/bot-v3/bots-with-tabs.md): タブとボットを連携させる。
* [ボットをテスト](~/resources/bot-v3/bots-test.md)する: 個人用またはチームの会話用にボットを追加して、ボットが動作しているのを確認します。

## <a name="see-also"></a>関連項目

[Bot Framework サンプル](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。
