---
title: Teams 開発者プラットフォーム
author: clearab
description: 開発者が Teams プラットフォームを使用して Microsoft Teams の機能を拡張およびカスタマイズする方法の概要について説明します。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 4af4d34ffa4581be6e69f6233d3eb356aa6a2a08
ms.sourcegitcommit: 52732714105fac07c331cd31e370a9685f45d3e1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "46874885"
---
# <a name="building-for-microsoft-teams"></a>Microsoft Teams の構築

Microsoft Teams アプリは、ユーザーが収集、学習、作業を徐々に行うことができるように、重要な情報、共通ツール、および信頼されたプロセスを提供します。

アプリは、ニーズに合わせて Teams を拡張する方法を示します。 Teams で新しいものを作成したり、お気に入りのアプリやサービスで機能を統合したりすることができます。

## <a name="what-can-teams-apps-do"></a>Teams アプリで実行できること

ユーザーは、一連のプラットフォーム [機能](capabilities-overview.md)を通じて Teams アプリを見つけて使用します。

単純な (通知を送信する) アプリもあれば、複雑なものもあります (患者の記録の表示)。 アプリを計画するときは、Teams がコラボレーションハブであることに注意してください。 最良の Teams アプリを使用すると、ユーザーが自分を表現し、連携しやすくなります。

### <a name="get-information-more-conveniently"></a>情報をより簡単に取得する

場合によっては、わかりやすくする必要があります。 重要な web ページを [タブ](doc-links/what-are-tabs.md)で表示します。これにより、チーム内の静的および動的なコンテンツについて全画面 web を利用できます。

![Teams クライアントでタブがどのように表示されるかを概念として表します。](doc-links/images/overview-tabs.png)

### <a name="share-links-without-switching-context"></a>コンテキストを切り替えずにリンクを共有する

情報を会話にプルし、Teams から退出させない。 たとえば、 [メッセージング拡張機能](doc-links/what-are-messaging-extensions.md) を使用すると、[メッセージの作成] ボックスを使用して、外部システムから簡単に digestible コンテンツを共有できます。

![Teams クライアントでメッセージング拡張機能がどのように表示されるかを概念的に表現する](doc-links\images\overview-messaging.png)

### <a name="turn-words-into-actions"></a>単語をアクションに変換する

会話では、多くの場合、何らかの処理 (注文の作成、自分のコードのレビューなど) が必要になります。 [Bot](doc-links/what-are-bots.md)は、Teams 内でこれらの種類のワークフローを直接開始できます。

![Teams クライアントでどのような bot が表示されるかを概念的に表現する](doc-links/images/overview-bots.png)

### <a name="communicate-with-external-apps-and-services"></a>外部のアプリとサービスと通信する

[受信 web フック](doc-links/what-are-webhooks-and-connectors.md#incoming-webhooks) は、別のアプリから Teams チャネルまたはチャットに通知を自動的に送信する簡単な方法です。 [送信 web フック](doc-links/what-are-webhooks-and-connectors.md#outgoing-webhooks)を使用すると、@mention を使用して web サービスにメッセージを送信できます。

![Teams クライアントでどのコネクタが表示されるかを概念として表します。](doc-links/images/overview-connectors.png)

### <a name="utilize-teams-data"></a>Teams データを利用する

[Teams 用の Microsoft GRAPH REST API](https://docs.microsoft.com/graph/teams-concept-overview)には、teams、チャネル、ユーザー、およびメッセージに関する情報へのアクセスが用意されており、アプリの機能を作成または拡張する際に役立ちます。

![「Teams 用の Microsoft Graph REST API の概念図](doc-links/images/overview-graph.png)
  
## <a name="start-building"></a>構築を開始する

   シンプルなアプリを作成し、よく使用されるいくつかの機能を追加することで、Teams の構築にすばやく慣れることができます。

   > [!div class="nextstepaction"]
   > [今すぐ最初のアプリを作成する](build-your-first-app/build-real-world-app.md)

### <a name="bring-it-all-together"></a>すべてをまとめる

   組織のお気に入りの web アプリケーション、サービス、およびシステムを Teams の共同作業機能でブレンディングすることにより、ユーザーのプロセスとワークフローを簡素化します。

   > [!div class="nextstepaction"]
   > [既存のアプリを統合する](doc-links/integrating-web-apps.md)

### <a name="trust-the-process"></a>プロセスを信頼する

   Teams プラットフォーム開発プロセス全体を理解し、組織または他のユーザーのためにアプリを効果的に計画、設計、構築、および発行します。

   > [!div class="nextstepaction"]
   > [アプリの計画を開始する](doc-links/extensibility-points.md)

### <a name="no-code-no-worries"></a>コードなし、心配なし

   魅力的なアプリを構築するためにプログラマである必要はありません。 Microsoft Power Platform を使用して、ほとんどコードを持たない Teams アプリを作成します。

   > [!div class="nextstepaction"]
   > [電源プラットフォームアプリのインポート](doc-links/importing-custom-microsoft-apps.md)

## <a name="resources"></a>リソース

* [Web サイトに [Teams に共有] ボタンを追加する](doc-links/share-to-teams.md)
* [Fluent UI デザインシステム](https://fluentsite.z22.web.core.windows.net/)
* [Microsoft Teams JavaScript クライアント SDK](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest)
* [JavaScript のボット FRAMEWORK sdk](https://github.com/Microsoft/botbuilder-js)および[bot framework sdk (.net](https://github.com/Microsoft/botbuilder-dotnet/) )
