---
title: 通話とオンライン会議ボット
description: 通話やオンライン会議Microsoft Teams、Microsoft Graph API を使用して、音声とビデオを使用してユーザーと対話する方法について説明します。
ms.topic: conceptual
localization_priority: Normal
keywords: 通話通話オーディオ ビデオ IVR 音声オンライン会議
ms.openlocfilehash: 578c10ab2566e8bbf51a2224b8d474fb74c92092ea815386865a4e28efe059c6
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2021
ms.locfileid: "57706799"
---
# <a name="calls-and-online-meetings-bots"></a>通話とオンライン会議ボット

ボットは、リアルタイムの音声Teams、画面共有を使用して、通話や会議を操作できます。 [通話およびGraph会議](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)用の Microsoft Teams API を使用すると、音声とビデオを使用してユーザーと対話してエクスペリエンスを強化できます。 これらの API を使用すると、次の新機能を追加できます。

* 対話型音声応答 (IVR)。
* 呼び出し制御。
* デスクトップとアプリの共有を含む、リアルタイムのオーディオストリームとビデオ ストリームへのアクセス。

これらの API を GraphアプリTeamsするには、ボットを作成し、追加の情報とアクセス許可を指定します。

また、リアルタイム メディア プラットフォームを使用すると、ボットはリアルタイムの音声、ビデオ、および画面共有を使用して、Teams通話や会議を操作できます。 音声またはビデオ通話やオンライン会議に参加するボットは、ボットの登録に使用Microsoft Teams機能が少ない通常のボットです。

2 Teams設定と、ボットの Microsoft App ID に対する Graph アクセス許可、およびテナント管理者の同意を含むアプリ マニフェストを使用すると、ボットを `supportsCalling` `supportsVideo` 登録できます。 Teams の通話と会議ボットを登録する場合、Webhook URL が記載されています。これは、ボットへのすべての着信呼び出しの Webhook エンドポイントです。 アプリケーションホスト型メディア ボットには、Microsoft が必要です。Graph。Communications.Calls.Media .NET ライブラリを使用してオーディオおよびビデオ メディア ストリームにアクセスし、ボットを Azure の Windows Server マシンまたは Windows Server ゲスト オペレーティング システム (OS) に展開する必要があります。 デバイス上のボットTeams、オーディオおよびビデオ コンテンツの特定のメディア形式のセットのみをサポートします。

ここで、いくつかの主要な概念、用語、および規則を理解する必要があります。

## <a name="terminologies"></a>Terminologies

次の主要な概念、用語、および規則は、通話とオンライン会議ボットの使用について説明します。

* 音声通話またはビデオ通話
* 通話の種類
* シグナル
* 通話とオンライン会議
* リアルタイム メディア

### <a name="audio-or-video-calls"></a>音声通話またはビデオ通話

オーディオまたはオーディオTeamsビデオの呼び出しは、完全に使用できます。 音声通話またはビデオ通話の代わりに、呼び出しという用語が使用されます。

### <a name="call-types"></a>通話の種類

呼び出しは、ユーザーとボットの間のピアツーピアか、ボットとグループ通話の 2 人以上のユーザーとの間のマルチパーティのいずれかです。

![呼び出しの種類](~/assets/images/calls-and-meetings/call-types.png)

呼び出しに必要なさまざまな呼び出しの種類とアクセス許可を次に示します。

* ユーザーは、ボットでピアツーピア呼び出しを開始したり、ボットを既存のマルチパーティ通話に招待することができます。 マルチパーティ呼び出しは、ユーザー インターフェイスでまだTeamsされていません。

    > [!NOTE]
    > ボットへのユーザーが開始した呼び出しは、現在、モバイル プラットフォームMicrosoft Teamsサポートされていません。

* Graphがボットとのピアツーピア呼び出しを開始する場合、アクセス許可は必要ありません。 ボットがマルチパーティ通話に参加したり、ボットがユーザーとのピアツーピア通話を開始したりするには、追加のアクセス許可が必要です。
* 呼び出しはピアツーピアとして開始され、最終的にはマルチパーティ通話になります。 ボットが適切なアクセス許可を持っている場合、ボットは他のユーザーを招待してマルチパーティ呼び出しを開始できます。 ボットにグループ通話に参加するためのアクセス許可が付与されていない場合、参加者が別の参加者を呼び出しに追加した場合、ボットは呼び出しから削除されます。

### <a name="signals"></a>シグナル

信号には、着信呼び出しと通話の 2 種類があります。 シグナルの異なる機能を次に示します。

* 着信呼び出しを受信するには、ボット設定にエンドポイントを入力します。 このエンドポイントは、着信呼び出しが開始されると通知を受け取ります。 通話に応答したり、拒否したり、他のユーザーにリダイレクトすることができます。

    ![呼び出しの処理](~/assets/images/calls-and-meetings/call-handling.png)

* ボットが呼び出し中の場合、ボットをミュートおよびミュート解除し、他の参加者とのビデオまたはデスクトップ コンテンツの共有を開始または停止する API があります。
* ボットは、参加者のリストにアクセスしたり、新しい参加者を招待したり、ミュートしたりできます。

### <a name="calls-and-online-meetings"></a>通話とオンライン会議

ユーザーのTeams、アドホック会議とスケジュール設定の 2 種類のオンライン会議があります。 ボットの観点から見ると、両方のオンライン会議は同じです。 ボットでは、オンライン会議は、一連の参加者間のマルチパーティ通話であり、会議の座標が含まれます。 会議の座標は、会議に関連付けられた、会議などの会議のメタデータ `botId` `chatId` `joinUrl` `startTime` `endTime` です。

### <a name="real-time-media"></a>リアルタイム メディア

ボットが通話またはオンライン会議に参加している場合は、音声ストリームとビデオ ストリームを処理する必要があります。 ユーザーが通話で話をする場合、Web カメラに自分自身を表示したり、会議で画面を表示したりすると、音声ストリームとビデオ ストリームとして表示されるボットに表示されます。 ボットが簡単なことを言いたい場合は、対話的な音声応答 (IVR) シナリオで **0** を押してオペレーターに到達するには、 を再生する必要があります。WAV ファイル。 総称して、これはメディアまたはリアルタイム メディアと呼ばれます。

リアルタイム メディアとは、以前に録音したオーディオやビデオの再生とは対照的に、メディアをリアルタイムで処理する必要があるシナリオを指します。 メディア ストリーム、特にリアルタイム メディア ストリームの処理は非常に複雑です。 Microsoft は、これらのシナリオを処理し、リアルタイム メディア処理の従来の負荷を可能な限り軽減するために、リアルタイム メディア プラットフォームを作成しました。 ボットが着信呼び出しに応答するか、新しい通話または既存の呼び出しに参加する場合は、メディアの処理方法をリアルタイム メディア プラットフォームに伝える必要があります。 IVR アプリケーションを構築する場合は、高価なオーディオ処理を Microsoft にオフロードできます。 または、ボットがメディア ストリームに直接アクセスする必要がある場合は、そのシナリオもサポートされます。 メディア処理には、次の 2 種類があります。

* **サービスホスト型メディア**: ボットは、呼び出しのルーティングやオーディオ処理の Microsoft リアルタイム メディア プラットフォームへのオフロードなど、アプリケーション ワークフローの管理に重点を置いて作業します。 サービスホスト型メディアでは、ボットを実装してホストするためのいくつかのオプションがあります。 サービスによりホストされるメディア ボットは、メディアをローカルで処理しないため、ステートレス サービスとして実装できます。 サービスホスト型メディア ボットでは、次の API を使用できます。

    * `PlayPrompt` オーディオ クリップを再生する場合。
    * `Record` オーディオ クリップの録音に使用します。
    * `SubscribeToTone` デュアル トーン多重周波数 (DTMF) トーンをサブスクライブする場合に使用します。

    たとえば、ユーザーが **0** を押してオペレーターに到達した場合を知る。

* **アプリケーションホスト型メディア**: ボットがメディアに直接アクセスするには、特定のアクセス許可Graphがあります。 ボットにアクセス許可が付与された後[](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/)、リアルタイム メディア ライブラリ、および SDK Graph呼び出し元は、リッチ[で](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/articles/index.html#graph-calling-sdk-and-stateful-client-builder)リアルタイムのメディアを構築し、ボットを呼び出すのに役立ちます。 アプリケーションによりホストされるボットは、Windows 環境でホストされる必要があります。 詳細については、「アプリケーションホスト [型メディア ボット」を参照してください](./requirements-considerations-application-hosted-media-bots.md)。

## <a name="code-sample"></a>コード サンプル

| **サンプルの名前** | **説明** | **Graph** |
|---------------|----------|--------|
| Graph通信 | Graph Microsoft の通信プラットフォームとやり取りするための通信を提供します。 | [表示](https://github.com/microsoftgraph/microsoft-graph-comms-samples) |
| 通話と会議ボット | このサンプル アプリでは、ボットが通話の作成、会議への参加、通話の転送を行う方法を説明します。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-calling-meeting/csharp) |

## <a name="see-also"></a>関連項目

- [GraphAPI リファレンス](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)

- [サンプル アプリ](https://github.com/microsoftgraph/microsoft-graph-comms-samples)

- [通話とオンライン会議をサポートするボットの登録](./registering-calling-bot.md)

- [Graphおよびオンライン会議ボットのアクセス許可の設定](./registering-calling-bot.md#add-graph-permissions)

- [コンピューターで通話とオンライン会議ボットを開発する方法](./debugging-local-testing-calling-meeting-bots.md)

- [アプリケーションホスト型メディア ボットの要件と考慮事項](./requirements-considerations-application-hosted-media-bots.md)

- [着信通知の処理に関する技術情報](./call-notifications.md)

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [リアルタイムのメディア通話と会議](~/bots/calls-and-meetings/real-time-media-concepts.md)
