---
title: 通話とオンライン会議のボット
description: Microsoft Teams アプリを使用して、Microsoft Graph Api を使用して通話やオンライン会議で音声とビデオを使用してユーザーと対話する方法について説明します。
keywords: 通話の音声ビデオ IVR 音声オンライン会議
ms.openlocfilehash: 03bd7e085908a49f070fe84aba87138ecabafb83
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674792"
---
# <a name="calls-and-online-meetings-bots"></a>通話とオンライン会議のボット

Microsoft [Graph api を呼び出しとオンライン会議に](/graph/api/resources/communications-api-overview?view=graph-rest-beta)追加することで、microsoft Teams アプリは音声とビデオを使用してさまざまな方法でユーザーと対話できるようになりました。 これらの Api を使用すると、対話式音声応答 (IVR)、通話コントロール、通話と会議のリアルタイム音声またはビデオストリーム (デスクトップとアプリの共有など) などの新しい機能を追加できます。

Microsoft Teams アプリでこれらの Microsoft Graph Api を使用するには、bot を作成し、別の場所で説明する追加情報とアクセス許可を指定します。最初に、中心概念、用語、および規則について理解することが重要です。

* **音声ビデオ通話。** Teams での通話は、完全に音声またはオーディオ + ビデオにすることができます。 簡潔にするために、「音声ビデオ通話」と言うことはありません。「call」と言っただけです。
* **通話の種類。** 通話は、ピアツーピア (人物と bot の間) またはマルチパーティ (グループ呼び出しでのお客様のボットと2人以上のユーザー) のいずれかです。
  ![通話の](~/assets/images/calls-and-meetings/call-types.png)種類:
  * ユーザーが bot とのピアツーピア通話を開始したり、既存のマルチパーティコールに bot を招待したりすることができます (後者は Microsoft Teams UI でまだ有効になっていません)。
  * ユーザーが bot とのピアツーピア通話を開始するために、Microsoft Graph のアクセス許可は必要ありませんが、bot がマルチパーティ通話に参加するため、またはユーザーとのピアツーピア通話をボットで開始するために、追加のアクセス許可が必要です。
  * 通話は、ピアツーピアとして開始し、マルチパーティにエスカレートできます。 Bot は、適切なアクセス許可を持っていれば、他のユーザーを招待することでこのエスカレーションを開始することができます。 Bot がグループ通話に参加するためのアクセス許可を持っておらず、1人の参加者が別のパーティを追加した場合は、その呼び出しから bot が削除されます。
* **リング.** シグナルには、着信通話と通話中の2種類があります。
  * 着信呼び出しを受信するには、ボット設定でエンドポイントを指定します。このエンドポイントは、着信呼び出しが到着したときに通知を受信します。 呼び出しに応答するか、拒否するか、または別の場所にリダイレクトすることができます。
  ![通話の種類](~/assets/images/calls-and-meetings/call-handling.png)
  * Bot が通話に参加している場合は、それ自体をミュートおよびミュート解除するための Api と、ビデオ/デスクトップコンテンツの共有を他の参加者との間で開始または停止することができます。
  * Bot は、参加者のリストにアクセスしたり、新しい参加者を招待したり、ミュートしたりすることもできます。
* **通話とオンライン会議。** Teams ユーザーの観点から見ると、2種類のオンライン会議があります。 ただし、bot の視点からは異なります。 Bot の場合、オンライン会議はマルチパーティの通話 (参加者のセット) と「ミーティングの座標`botId`」 (会議のメタデータとも呼ば`chatId`れます) と、会議に関連付けられ`joinUrl` `startTime` / `endTime`ていることを考えることができます。
* **リアルタイムメディア。** Bot が通話またはオンライン会議に参加している場合は、音声およびビデオストリームを処理する必要があります。 ユーザーが電話をかけたり、webcam で自分を表示したり、会議で自分の画面を表示したりすると、bot はこれを音声またはビデオストリームとして認識します。 Bot が何かを言ったり、画面の内容を表示したりしたい場合は、音声またはビデオストリームが必要です。 「IVR (対話式音声応答)」のシナリオでは、bot が単純なものであっても、を再生することは、を再生することを意味します。WAV ファイル。 これは、_メディアまたは__リアルタイムメディア_として参照されています (以前録音された音声/ビデオを再生するのではなく、リアルタイムで処理する必要がある場合)。 従来、メディアストリーム (特にリアルタイムメディアストリーム) の処理は、開発者にとって非常に複雑になっていました。 Microsoft では、このようなユースケースを処理するために_リアルタイムメディアプラットフォーム_を作成し、リアルタイムメディア処理の従来の "大量発生" をできるだけオフロードするようにしています。  ボットが着信通話に応答するか、新規通話または既存の通話に参加する場合、ボットは Real-time Media Platform に対しメディアの処理方法を通知する必要があります。 IVR アプリケーションを構築している場合は、高コストのオーディオ処理を Microsoft にオフロードすることができます。 または、ボットがメディアストリームへの直接アクセスを必要とする場合は、そのシナリオもサポートします。 メディア処理には、次の2種類があります。
  * **サービスホストメディア。** Bot は、アプリケーションワークフロー (ルーティング呼び出しなど) を管理し、Microsoft のリアルタイムメディアプラットフォームへのオーディオ処理をオフロードすることに重点を置いています。 サービスホスト型メディアでは、ボットを実装してホストするためのいくつかのオプションがあります。 サービスホスト型メディアボットは、メディアをローカルに処理しないため、ステートレスサービスとして実装できます。 サービスホスト型メディアのボットは、オーディオクリップ`PlayPrompt`の再生、 `Record`オーディオクリップの録音、または`SubscribeToTone` DTMF トーンの定期処理 (たとえば、ユーザーが0を押してオペレーターに到達した場合に知らせる) などの api を使用できます。
  * **アプリケーションホスト型メディア。** Bot がメディアに直接アクセスできるようにするためには、特定のグラフアクセス許可が必要ですが、bot がこれを持っていれば、[リアルタイムメディアライブラリ](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/)と[Graph 通話 SDK](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/articles/index.html#graph-calling-sdk-and-stateful-client-builder)を使用して、多機能なリアルタイムメディアを構築したり、ボットを呼び出したりすることができます。 アプリケーションホストボットは、Windows 環境でホストされている必要があります。詳細については、[こちら](./requirements-considerations-application-hosted-media-bots.md)を参照してください。

## <a name="further-reading"></a>参考資料

通話とオンライン会議のボットを作成およびテストする方法については、以下の情報を参照してください。

* [Graph API リファレンス](/graph/api/resources/communications-api-overview?view=graph-rest-beta)
* [サンプルアプリ](https://github.com/microsoftgraph/microsoft-graph-comms-samples)
* 通話とオンライン会議の機能を[サポートするボットを登録](./registering-calling-bot.md)する、および[Microsoft Graph のアクセス許可を使用](/registering-calling-bot.md#add-microsoft-graph-permissions)する
* [ローカル PC で通話およびオンライン会議のボットを開発する方法](./debugging-local-testing-calling-meeting-bots.md)
* [リアルタイムメディア処理に関する詳細](./real-time-media-concepts.md)と、[アプリケーションホスト型メディアをサポートするために必要なもの](./requirements-considerations-application-hosted-media-bots.md)
* [着信呼び出し通知の処理に関する技術情報](./call-notifications.md)
