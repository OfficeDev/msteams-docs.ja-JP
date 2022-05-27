---
title: 通話とオンライン会議のボット
description: Microsoft Teams アプリが通話やオンライン会議に Microsoft Graph API と、音声及びビデオを使用してユーザーと対話する方法、そしてリアルタイム メディア ストリームについて説明します
ms.topic: conceptual
ms.localizationpriority: medium
keywords: 発信 通話 音声ビデオ IVR 音声オンライン会議 リアルタイム メディア ストリーム ボット
ms.openlocfilehash: 48c5283a1552c2f04651fe67254def0e6d60a8e6
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2022
ms.locfileid: "65756731"
---
# <a name="calls-and-online-meetings-bots"></a>通話とオンライン会議のボット

ボットは、リアルタイムの音声、ビデオ、画面共有を使用して、Teams 通話や会議と対話できます。 [通話とオンライン会議用の Microsoft Graph API](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true) を使用して、Teams アプリは音声とビデオを使用してユーザーと対話し、エクスペリエンスを強化しました。 これらの API を使用すると、次の新機能を追加できます:

* 自動音声応答 (IVR)。
* 通話コントロール。
* デスクトップやアプリの共有を含む、リアルタイムのオーディオとビデオのストリームを利用しましょう。

Teams アプリでこれらの Graph API を使用するには、ボットを作成し、いくつかの追加情報とアクセス許可を指定します。

さらに、リアルタイム メディア プラットフォームを使用すると、ボットはリアルタイムの音声、ビデオ、画面共有を使用して Teams 通話や会議と対話できます。 音声通話やビデオ通話、オンライン会議に同席するボットは、ボットの登録に使用される少数の追加機能を伴う通常の Microsoft Teams ボットです。

Teams アプリ マニフェストには、2 つの追加設定`supportsCalling`と`supportsVideo`、ボットの Microsoft アプリ ID について Graph アクセス許可が含まれており、あなたがボットを登録できるようになることについて、テナント管理者が同意することになります。 Teams 通話と会議のボットを登録する際に、Webhook URL がメンションされ、これはボットへのすべての着信通話の Webhook エンドポイントです。 アプリケーションでホストされるメディア ボットでは、オーディオ およびビデオ メディア ストリームにアクセスするために Microsoft.Graph.Communications.Calls.Media .NET ライブラリが必要で、ボットは Windows Server マシンまたは Azure の Windows Server ゲスト オペレーティング システム (OS) にデプロイする必要があります。 Teams上のボットでは、オーディオ コンテンツとビデオ コンテンツの特定のメディア形式のセットのみがサポートされます。

ここで、いくつかの主要な概念、専門用語、および規則を理解する必要があります。

## <a name="terminologies"></a>専門用語集

次の主要な概念、用語、および規則は、通話とオンライン会議ボットの使用を通じてあなたをガイドします。

* 音声通話またはビデオ通話
* 通話の種類
* 信号
* 通話とオンライン会議
* リアルタイム メディア

### <a name="audio-or-video-calls"></a>音声通話またはビデオ通話

Teams での通話は、純粋に音声のみ、または音声とビデオにすることができます。 音声またはビデオ通話の代わりに、通話という用語が使用されます。

### <a name="call-types"></a>通話の種類

通話は、ユーザーとボットの間のピア ツー ピア、またはグループ通話内の 2 人以上のユーザーとボットの間のマルチパーティのいずれかです。

:::image type="content" source="~/assets/images/calls-and-meetings/call-types.png" alt-text="通話タイプ"border="true":::

通話に必要なさまざまな通話タイプとアクセス許可を次に示します:

* ユーザーは、ボットの支援でピア ツー ピア通話を開始したり、ボットを既存のマルチパーティ通話に招待したりできます。 マルチパーティ呼び出しは、Teams ユーザー インターフェイスではまだ有効になっていません。

    > [!NOTE]
    > ユーザーが開始するボットへの通話は、現在 Microsoft Teams モバイル プラットフォームではサポートされていません。

* Graphアクセス許可は、ユーザーがボットとのピアツーピア呼び出しを開始するために必要ありません。 ボットがマルチパーティ通話に参加したり、ボットがユーザーとのピア ツー ピア通話を開始したりするには、ボットに追加のアクセス許可が必要です。
* 通話はピア ツー ピアとして開始し、最終的にはマルチパーティ通話になります。 ボットに適切なアクセス許可が与えられながら、ボットは他のユーザーを招待することでマルチパーティ通話を開始できます。 ボットにグループ通話に参加するアクセス許可がなく、参加者が別の参加者を呼び出しに追加した場合、ボットは通話から削除されます。

### <a name="signals"></a>信号

着信と通話時通信の 2 種類の信号があります。 以下は信号のさまざまな機能です:

* 着信を受信するには、ボットの設定にエンドポイントを 1 つ入力します。 このエンドポイントは、着信が開始されたときに通知を受け取ります。 通話に応答したり、それを拒否したり、他のユーザーにリダイレクトしたりできます。

     :::image type="content" source="~/assets/images/calls-and-meetings/call-handling.png" alt-text="通話処理"border="true":::

* ボットが通話中の場合、ボットをミュートしたりそれを解除したり、ビデオやデスクトップ コンテンツを他の参加者と共有したり共有を停止したりするための API があります。
* ボットは、参加者の一覧にアクセスし、新しい参加者を招待し、ミュートすることもできます。

### <a name="calls-and-online-meetings"></a>通話とオンライン会議

Teams ユーザーの観点からは、随意開催と計画開催の 2 種類のオンライン会議があります。 ボットの観点から見ると、両方のオンライン会議は同一です。 1 つのボットに対して、オンライン会議は参加者の組との間のマルチパーティ通話であり、会議の調整情報が含まれます。 会議の調整情報は、会議に関連付けられている`botId`、`chatId`、`joinUrl`、`startTime`、または`endTime`などの会議のメタデータです。

### <a name="real-time-media"></a>リアルタイム メディア

ボットが通話またはオンライン会議に参加している場合は、音声ストリームとビデオ ストリームを処理する必要があります。 ユーザーが通話中に会話したり、Web カメラで自分を表示したり、会議で画面を表示したりすると、音声ストリームとビデオ ストリームとして表示されるボットに表示されます。 ボットがしごく単純に何かを言いたい場合、 **0 を押して対話型音声応答 (IVR) シナリオでオペレーター** に到達するには、.WAV ファイルを再生する必要があります。 これらを総称して、メディアまたはリアルタイム メディアと呼ばれます。

リアルタイム メディアとは、以前に記録したオーディオやビデオの再生とは対照的に、メディアをリアルタイムで処理する必要があるシナリオを指します。 メディア ストリーム (特にリアルタイム メディア ストリーム) の処理は複雑です。 Microsoft は、これらのシナリオを処理し、負荷の重い従来のリアルタイム メディア処理の負担を可能な限り取り除くために、リアルタイム メディア プラットフォームを作成しました。 ボットが着信に応答するか、新規または既存の通話に参加する場合は、リアルタイム メディア プラットフォームにメディアの処理方法を伝える必要があります。 IVR アプリケーションを構築する場合は、高価なオーディオ処理を Microsoft にオフロードできます。 または、ボットでメディア ストリームへの直接のアクセスが必要な場合は、そのシナリオもサポートされます。 メディア処理には、次の 2 種類があります:

* **サービスでホストされるメディア**: ボットは、通話のルーティングや Microsoft リアルタイム メディア プラットフォームへのオーディオ処理のオフロードなど、アプリケーション ワークフローの管理に重点を置きます。 サービスによりホストされるメディアを使用すると、ボットを実装しホストするためのさまざまなオプションが使用できるようになります。 サービスでホストされるメディア ボットは、メディアをローカルで処理しないため、ステートレス サービスとして実装できます。 サービスホスト型メディア ボットでは、次の API を使用できます:

  * `PlayPrompt` オーディオ クリップを再生するため。
  * `Record` オーディオ クリップを記録するため。
  * `SubscribeToTone` デュアル トーン周波数多重 (DTMF) トーンにサービス登録するため。

    たとえば、ユーザーがいつ **0** を押してオペレーターに到達したかを把握します。

* **アプリケーション ホスト型メディア**: ボットがメディアに直接アクセスするには、特定の Graph アクセス許可が必要です。 ボットにアクセス許可が付与された後、[リアルタイム メディア ライブラリ](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/)と [Graph 通話 SDK](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/articles/index.html#graph-calling-sdk-and-stateful-client-builder) は、リッチでリアルタイムのメディアを構築し、ボットとの通話に役立ちます。 アプリケーションによりホストされるボットは、Windows 環境でホストされる必要があります。 詳細については、[アプリケーションでホストされるメディア ボット](./requirements-considerations-application-hosted-media-bots.md)に関するページを参照してください。

## <a name="code-sample"></a>コード サンプル

| **サンプルの名前** | **説明** | **Graph** |
|---------------|----------|--------|
| Graph 通話 | Microsoft の通話プラットフォームと対話するための Graph 通話。 | [表示](https://github.com/microsoftgraph/microsoft-graph-comms-samples) |

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [リアルタイムのメディア通話と会議](~/bots/calls-and-meetings/real-time-media-concepts.md)

## <a name="see-also"></a>関連項目

* [Graph API リファレンス](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)
* [サンプル アプリ](https://github.com/microsoftgraph/microsoft-graph-comms-samples)
* [通話とオンライン会議をサポートするボットを登録する](./registering-calling-bot.md)
* [通話とオンライン会議ボットの Graph アクセス許可](./registering-calling-bot.md#add-graph-permissions)
* [コンピューターで通話とオンライン会議ボットを開発する方法](./debugging-local-testing-calling-meeting-bots.md)
* [アプリケーションでホストされるメディア ボットの要件と考察](./requirements-considerations-application-hosted-media-bots.md)
* [着信通知の処理に関する技術情報](./call-notifications.md)
* [自動応答を設定する](/microsoftteams/create-a-phone-system-auto-attendant)
* [Android および Teams ビデオ電話デバイスの Microsoft Teams Rooms 自動応答を設定する](/microsoftteams/set-up-auto-answer-on-teams-android)
* [Teams レコーディング ポリシー](/MicrosoftTeams/teams-recording-policy)
* [Microsoft Graph で通信 API を操作する](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)
