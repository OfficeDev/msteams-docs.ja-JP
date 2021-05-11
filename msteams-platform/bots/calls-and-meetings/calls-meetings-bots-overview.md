---
title: 通話とオンライン会議ボット
description: 通話やオンライン会議Microsoft Teams、Microsoft Graph API を使用して、音声とビデオを使用してユーザーと対話する方法について説明します。
ms.topic: conceptual
localization_priority: Normal
keywords: 通話通話オーディオ ビデオ IVR 音声オンライン会議
ms.openlocfilehash: d4cec30e110eed5f73929305cc43b84eed4d7524
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058314"
---
# <a name="calls-and-online-meetings-bots"></a><span data-ttu-id="a0d09-104">通話とオンライン会議ボット</span><span class="sxs-lookup"><span data-stu-id="a0d09-104">Calls and online meetings bots</span></span>

> [!NOTE]
> <span data-ttu-id="a0d09-105">通話とオンライン会議ボットのサポートは、現在、モバイル プラットフォームMicrosoft Teamsサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="a0d09-105">Support for calls and online meeting bots is currently not supported on the Microsoft Teams mobile platform.</span></span>

<span data-ttu-id="a0d09-106">ボットは、リアルタイムの音声Teams、画面共有を使用して、通話や会議を操作できます。</span><span class="sxs-lookup"><span data-stu-id="a0d09-106">Bots can interact with Teams calls and meetings using real-time voice, video, and screen sharing.</span></span> <span data-ttu-id="a0d09-107">[通話およびGraph会議](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)用の Microsoft Teams API を使用すると、音声とビデオを使用してユーザーと対話してエクスペリエンスを強化できます。</span><span class="sxs-lookup"><span data-stu-id="a0d09-107">With [Microsoft Graph APIs for calls and online meetings](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true), Teams apps can now interact with users using voice and video to enhance the experience.</span></span> <span data-ttu-id="a0d09-108">これらの API を使用すると、次の新機能を追加できます。</span><span class="sxs-lookup"><span data-stu-id="a0d09-108">These APIs allow you to add the following new features:</span></span>

* <span data-ttu-id="a0d09-109">対話型音声応答 (IVR)。</span><span class="sxs-lookup"><span data-stu-id="a0d09-109">Interactive voice response (IVR).</span></span>
* <span data-ttu-id="a0d09-110">呼び出し制御。</span><span class="sxs-lookup"><span data-stu-id="a0d09-110">Call control.</span></span>
* <span data-ttu-id="a0d09-111">デスクトップとアプリの共有を含む、リアルタイムのオーディオストリームとビデオ ストリームへのアクセス。</span><span class="sxs-lookup"><span data-stu-id="a0d09-111">Access to real-time audio and video streams, including desktop and app sharing.</span></span>

<span data-ttu-id="a0d09-112">これらの API を GraphアプリTeamsするには、ボットを作成し、追加の情報とアクセス許可を指定します。</span><span class="sxs-lookup"><span data-stu-id="a0d09-112">To use these Graph APIs in a Teams app, you create a bot and specify some additional information and permissions.</span></span>

<span data-ttu-id="a0d09-113">また、リアルタイム メディア プラットフォームを使用すると、ボットはリアルタイムの音声、ビデオ、および画面共有を使用して、Teams通話や会議を操作できます。</span><span class="sxs-lookup"><span data-stu-id="a0d09-113">In addition, the Real-time Media Platform enables bots to interact with Teams calls and meetings using real-time voice, video, and screen sharing.</span></span> <span data-ttu-id="a0d09-114">音声またはビデオ通話やオンライン会議に参加するボットは、ボットの登録に使用Microsoft Teams機能が少ない通常のボットです。</span><span class="sxs-lookup"><span data-stu-id="a0d09-114">A bot that participates in audio or video calls and online meetings is a regular Microsoft Teams bot with few extra features used to register the bot.</span></span>

<span data-ttu-id="a0d09-115">2 Teams設定と、ボットの Microsoft App ID に対する Graph アクセス許可、およびテナント管理者の同意を含むアプリ マニフェストを使用すると、ボットを `supportsCalling` `supportsVideo` 登録できます。</span><span class="sxs-lookup"><span data-stu-id="a0d09-115">The Teams app manifest with two additional settings `supportsCalling` and `supportsVideo`, Graph permissions for your bot's Microsoft App ID, and tenant admin consent enable you to register the bot.</span></span> <span data-ttu-id="a0d09-116">Teams の通話と会議ボットを登録する場合、Webhook URL が記載されています。これは、ボットへのすべての着信呼び出しの Webhook エンドポイントです。</span><span class="sxs-lookup"><span data-stu-id="a0d09-116">In registering a calls and meetings bot for Teams, the Webhook URL is mentioned, which is the webhook endpoint for all incoming calls to your bot.</span></span> <span data-ttu-id="a0d09-117">アプリケーションホスト型メディア ボットには、Microsoft が必要です。Graph。Communications.Calls.Media .NET ライブラリを使用してオーディオおよびビデオ メディア ストリームにアクセスし、ボットを Azure の Windows Server マシンまたは Windows Server ゲスト オペレーティング システム (OS) に展開する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a0d09-117">An application-hosted media bot requires the Microsoft.Graph.Communications.Calls.Media .NET library to access the audio and video media streams, and the bot must be deployed on a Windows Server machine or Windows Server guest Operating System (OS) in Azure.</span></span> <span data-ttu-id="a0d09-118">デバイス上のボットTeams、オーディオおよびビデオ コンテンツの特定のメディア形式のセットのみをサポートします。</span><span class="sxs-lookup"><span data-stu-id="a0d09-118">Bots on Teams supports only a specific set of media formats for audio and video content.</span></span>

<span data-ttu-id="a0d09-119">ここで、いくつかの主要な概念、用語、および規則を理解する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a0d09-119">Now, you must understand some core concepts, terminology, and conventions.</span></span>

## <a name="terminologies"></a><span data-ttu-id="a0d09-120">Terminologies</span><span class="sxs-lookup"><span data-stu-id="a0d09-120">Terminologies</span></span>

<span data-ttu-id="a0d09-121">次の主要な概念、用語、および規則は、通話とオンライン会議ボットの使用について説明します。</span><span class="sxs-lookup"><span data-stu-id="a0d09-121">The following core concepts, terminology, and conventions guide you through the use of calls and online meetings bots:</span></span>

* <span data-ttu-id="a0d09-122">音声通話またはビデオ通話</span><span class="sxs-lookup"><span data-stu-id="a0d09-122">Audio or video calls</span></span>
* <span data-ttu-id="a0d09-123">通話の種類</span><span class="sxs-lookup"><span data-stu-id="a0d09-123">Call types</span></span>
* <span data-ttu-id="a0d09-124">シグナル</span><span class="sxs-lookup"><span data-stu-id="a0d09-124">Signals</span></span>
* <span data-ttu-id="a0d09-125">通話とオンライン会議</span><span class="sxs-lookup"><span data-stu-id="a0d09-125">Calls and online meetings</span></span>
* <span data-ttu-id="a0d09-126">リアルタイム メディア</span><span class="sxs-lookup"><span data-stu-id="a0d09-126">Real-time media</span></span>

### <a name="audio-or-video-calls"></a><span data-ttu-id="a0d09-127">音声通話またはビデオ通話</span><span class="sxs-lookup"><span data-stu-id="a0d09-127">Audio or video calls</span></span>

<span data-ttu-id="a0d09-128">オーディオまたはオーディオTeamsビデオの呼び出しは、完全に使用できます。</span><span class="sxs-lookup"><span data-stu-id="a0d09-128">Calls in Teams can be purely audio or audio and video.</span></span> <span data-ttu-id="a0d09-129">音声通話またはビデオ通話の代わりに、呼び出しという用語が使用されます。</span><span class="sxs-lookup"><span data-stu-id="a0d09-129">Instead of audio or video call, the term call is used.</span></span>

### <a name="call-types"></a><span data-ttu-id="a0d09-130">通話の種類</span><span class="sxs-lookup"><span data-stu-id="a0d09-130">Call types</span></span>

<span data-ttu-id="a0d09-131">呼び出しは、ユーザーとボットの間のピアツーピアか、ボットとグループ通話の 2 人以上のユーザーとの間のマルチパーティのいずれかです。</span><span class="sxs-lookup"><span data-stu-id="a0d09-131">Calls are either peer-to-peer between a person and your bot, or multiparty between your bot and two or more people in a group call.</span></span>

![呼び出しの種類](~/assets/images/calls-and-meetings/call-types.png)

<span data-ttu-id="a0d09-133">呼び出しに必要なさまざまな呼び出しの種類とアクセス許可を次に示します。</span><span class="sxs-lookup"><span data-stu-id="a0d09-133">Following are the different call types and permissions required for the call:</span></span>

* <span data-ttu-id="a0d09-134">ユーザーは、ボットでピアツーピア呼び出しを開始したり、ボットを既存のマルチパーティ通話に招待することができます。</span><span class="sxs-lookup"><span data-stu-id="a0d09-134">A user can initiate a peer-to-peer call with your bot or invite your bot into an existing multiparty call.</span></span> <span data-ttu-id="a0d09-135">マルチパーティ呼び出しは、ユーザー インターフェイスでまだTeamsされていません。</span><span class="sxs-lookup"><span data-stu-id="a0d09-135">The multiparty call is not enabled yet in the Teams user interface.</span></span>
* <span data-ttu-id="a0d09-136">Graphがボットとのピアツーピア呼び出しを開始する場合、アクセス許可は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="a0d09-136">Graph permissions are not necessary for a user to initiate a peer-to-peer call with your bot.</span></span> <span data-ttu-id="a0d09-137">ボットがマルチパーティ通話に参加したり、ボットがユーザーとのピアツーピア通話を開始したりするには、追加のアクセス許可が必要です。</span><span class="sxs-lookup"><span data-stu-id="a0d09-137">Additional permissions are needed for your bot to participate in a multiparty call, or for your bot to initiate a peer-to-peer call with a user.</span></span>
* <span data-ttu-id="a0d09-138">呼び出しはピアツーピアとして開始され、最終的にはマルチパーティ通話になります。</span><span class="sxs-lookup"><span data-stu-id="a0d09-138">A call can start as peer-to-peer and eventually become a multiparty call.</span></span> <span data-ttu-id="a0d09-139">ボットが適切なアクセス許可を持っている場合、ボットは他のユーザーを招待してマルチパーティ呼び出しを開始できます。</span><span class="sxs-lookup"><span data-stu-id="a0d09-139">Your bot can initiate multiparty calls by inviting others, provided your bot has the proper permissions.</span></span> <span data-ttu-id="a0d09-140">ボットにグループ通話に参加するためのアクセス許可が付与されていない場合、参加者が別の参加者を呼び出しに追加した場合、ボットは呼び出しから削除されます。</span><span class="sxs-lookup"><span data-stu-id="a0d09-140">If your bot does not have permissions to participate in group calls and if a participant adds another participant to the call, your bot is dropped from the call.</span></span>

### <a name="signals"></a><span data-ttu-id="a0d09-141">シグナル</span><span class="sxs-lookup"><span data-stu-id="a0d09-141">Signals</span></span>

<span data-ttu-id="a0d09-142">信号には、着信呼び出しと通話の 2 種類があります。</span><span class="sxs-lookup"><span data-stu-id="a0d09-142">There are two types of signals, incoming call and in-call.</span></span> <span data-ttu-id="a0d09-143">シグナルの異なる機能を次に示します。</span><span class="sxs-lookup"><span data-stu-id="a0d09-143">Following are the different features of signals:</span></span>

* <span data-ttu-id="a0d09-144">着信呼び出しを受信するには、ボット設定にエンドポイントを入力します。</span><span class="sxs-lookup"><span data-stu-id="a0d09-144">To receive an incoming call, you enter an endpoint in your bot settings.</span></span> <span data-ttu-id="a0d09-145">このエンドポイントは、着信呼び出しが開始されると通知を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="a0d09-145">This endpoint receives a notification when an incoming call is initiated.</span></span> <span data-ttu-id="a0d09-146">通話に応答したり、拒否したり、他のユーザーにリダイレクトすることができます。</span><span class="sxs-lookup"><span data-stu-id="a0d09-146">You can answer the call, reject it, or redirect it to someone else.</span></span>

    ![呼び出しの処理](~/assets/images/calls-and-meetings/call-handling.png)

* <span data-ttu-id="a0d09-148">ボットが呼び出し中の場合、ボットをミュートおよびミュート解除し、他の参加者とのビデオまたはデスクトップ コンテンツの共有を開始または停止する API があります。</span><span class="sxs-lookup"><span data-stu-id="a0d09-148">When a bot is in a call, there are APIs for muting and unmuting the bot and to start or stop sharing video or desktop content with other participants.</span></span>
* <span data-ttu-id="a0d09-149">ボットは、参加者のリストにアクセスしたり、新しい参加者を招待したり、ミュートしたりできます。</span><span class="sxs-lookup"><span data-stu-id="a0d09-149">The bot can also access the list of participants, invite new participants, and mute them.</span></span>

### <a name="calls-and-online-meetings"></a><span data-ttu-id="a0d09-150">通話とオンライン会議</span><span class="sxs-lookup"><span data-stu-id="a0d09-150">Calls and online meetings</span></span>

<span data-ttu-id="a0d09-151">ユーザーのTeams、アドホック会議とスケジュール設定の 2 種類のオンライン会議があります。</span><span class="sxs-lookup"><span data-stu-id="a0d09-151">From a Teams user's perspective, there are two kinds of online meetings, ad hoc and scheduled.</span></span> <span data-ttu-id="a0d09-152">ボットの観点から見ると、両方のオンライン会議は同じです。</span><span class="sxs-lookup"><span data-stu-id="a0d09-152">From a bot's perspective, both online meetings are the same.</span></span> <span data-ttu-id="a0d09-153">ボットでは、オンライン会議は、一連の参加者間のマルチパーティ通話であり、会議の座標が含まれます。</span><span class="sxs-lookup"><span data-stu-id="a0d09-153">To a bot, an online meeting is a multiparty call between a set of participants and includes meeting coordinates.</span></span> <span data-ttu-id="a0d09-154">会議の座標は、会議に関連付けられた、会議などの会議のメタデータ `botId` `chatId` `joinUrl` `startTime` `endTime` です。</span><span class="sxs-lookup"><span data-stu-id="a0d09-154">Meeting coordinates are the metadata for the meeting including `botId`, `chatId` associated with the meeting, `joinUrl`, `startTime` or `endTime`, and so on.</span></span>

### <a name="real-time-media"></a><span data-ttu-id="a0d09-155">リアルタイム メディア</span><span class="sxs-lookup"><span data-stu-id="a0d09-155">Real-time media</span></span>

<span data-ttu-id="a0d09-156">ボットが通話またはオンライン会議に参加している場合は、音声ストリームとビデオ ストリームを処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a0d09-156">When a bot is participating in a call or online meeting, it must deal with audio and video streams.</span></span> <span data-ttu-id="a0d09-157">ユーザーが通話で話をする場合、Web カメラに自分自身を表示したり、会議で画面を表示したりすると、音声ストリームとビデオ ストリームとして表示されるボットに表示されます。</span><span class="sxs-lookup"><span data-stu-id="a0d09-157">When users talk on a call, show themselves on a webcam, or present their screens in a meeting, to a bot it is shown as audio and video streams.</span></span> <span data-ttu-id="a0d09-158">ボットが簡単なことを言いたい場合は、対話的な音声応答 (IVR) シナリオで **0** を押してオペレーターに到達するには、 を再生する必要があります。WAV ファイル。</span><span class="sxs-lookup"><span data-stu-id="a0d09-158">If a bot wants to say something as simple as, **press 0 to reach the operator** in an interactive voice response (IVR) scenario, it requires playing a .WAV file.</span></span> <span data-ttu-id="a0d09-159">総称して、これはメディアまたはリアルタイム メディアと呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="a0d09-159">Collectively, this is referred to as media or real-time media.</span></span>

<span data-ttu-id="a0d09-160">リアルタイム メディアとは、以前に録音したオーディオやビデオの再生とは対照的に、メディアをリアルタイムで処理する必要があるシナリオを指します。</span><span class="sxs-lookup"><span data-stu-id="a0d09-160">Real-time media refers to scenarios where media must be processed in real-time, as opposed to playback of previously recorded audio or video.</span></span> <span data-ttu-id="a0d09-161">メディア ストリーム、特にリアルタイム メディア ストリームの処理は非常に複雑です。</span><span class="sxs-lookup"><span data-stu-id="a0d09-161">Dealing with media streams, particularly real-time media streams, is extremely complex.</span></span> <span data-ttu-id="a0d09-162">Microsoft は、これらのシナリオを処理し、リアルタイム メディア処理の従来の負荷を可能な限り軽減するために、リアルタイム メディア プラットフォームを作成しました。</span><span class="sxs-lookup"><span data-stu-id="a0d09-162">Microsoft has created the Real-time Media Platform to handle these scenarios and to offload as much of the traditional heavy lifting of real-time media processing as possible.</span></span> <span data-ttu-id="a0d09-163">ボットが着信呼び出しに応答するか、新しい通話または既存の呼び出しに参加する場合は、メディアの処理方法をリアルタイム メディア プラットフォームに伝える必要があります。</span><span class="sxs-lookup"><span data-stu-id="a0d09-163">When the bot answers an incoming call or joins a new or existing call, it needs to tell the Real-time Media Platform how media is handled.</span></span> <span data-ttu-id="a0d09-164">IVR アプリケーションを構築する場合は、高価なオーディオ処理を Microsoft にオフロードできます。</span><span class="sxs-lookup"><span data-stu-id="a0d09-164">If you are building an IVR application, you can offload the expensive audio processing to Microsoft.</span></span> <span data-ttu-id="a0d09-165">または、ボットがメディア ストリームに直接アクセスする必要がある場合は、そのシナリオもサポートされます。</span><span class="sxs-lookup"><span data-stu-id="a0d09-165">Alternately, if your bot requires direct access to media streams, that scenario is also supported.</span></span> <span data-ttu-id="a0d09-166">メディア処理には、次の 2 種類があります。</span><span class="sxs-lookup"><span data-stu-id="a0d09-166">There are two types of media processing:</span></span>

* <span data-ttu-id="a0d09-167">**サービスホスト型メディア**: ボットは、呼び出しのルーティングやオーディオ処理の Microsoft リアルタイム メディア プラットフォームへのオフロードなど、アプリケーション ワークフローの管理に重点を置いて作業します。</span><span class="sxs-lookup"><span data-stu-id="a0d09-167">**Service-hosted media**: Bots focus on managing application workflow, such as routing calls and offload audio processing to the Microsoft Real-time Media Platform.</span></span> <span data-ttu-id="a0d09-168">サービスホスト型メディアでは、ボットを実装してホストするためのいくつかのオプションがあります。</span><span class="sxs-lookup"><span data-stu-id="a0d09-168">With service-hosted media, you have several options to implement and host your bot.</span></span> <span data-ttu-id="a0d09-169">サービスによりホストされるメディア ボットは、メディアをローカルで処理しないため、ステートレス サービスとして実装できます。</span><span class="sxs-lookup"><span data-stu-id="a0d09-169">A service-hosted media bot can be implemented as a stateless service as it does not process media locally.</span></span> <span data-ttu-id="a0d09-170">サービスホスト型メディア ボットでは、次の API を使用できます。</span><span class="sxs-lookup"><span data-stu-id="a0d09-170">Service-hosted media bots can use the following APIs:</span></span>

    * <span data-ttu-id="a0d09-171">`PlayPrompt` オーディオ クリップを再生する場合。</span><span class="sxs-lookup"><span data-stu-id="a0d09-171">`PlayPrompt` for playing an audio clip.</span></span>
    * <span data-ttu-id="a0d09-172">`Record` オーディオ クリップの録音に使用します。</span><span class="sxs-lookup"><span data-stu-id="a0d09-172">`Record` for recording audio clips.</span></span>
    * <span data-ttu-id="a0d09-173">`SubscribeToTone` デュアル トーン多重周波数 (DTMF) トーンをサブスクライブする場合に使用します。</span><span class="sxs-lookup"><span data-stu-id="a0d09-173">`SubscribeToTone` for subscribing to dual tone multiple frequency (DTMF) tones.</span></span>

    <span data-ttu-id="a0d09-174">たとえば、ユーザーが **0** を押してオペレーターに到達した場合を知る。</span><span class="sxs-lookup"><span data-stu-id="a0d09-174">For example, knowing when a user has pressed **0** to reach the operator.</span></span>

* <span data-ttu-id="a0d09-175">**アプリケーションホスト型メディア**: ボットがメディアに直接アクセスするには、特定のアクセス許可Graphがあります。</span><span class="sxs-lookup"><span data-stu-id="a0d09-175">**Application-hosted media**: For a bot to get direct access to the media, it needs a specific Graph permission.</span></span> <span data-ttu-id="a0d09-176">ボットにアクセス許可が付与された後[](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/)、リアルタイム メディア ライブラリ、および SDK Graph呼び出し元は、リッチ[で](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/articles/index.html#graph-calling-sdk-and-stateful-client-builder)リアルタイムのメディアを構築し、ボットを呼び出すのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="a0d09-176">After your bot has the permission, the [Real-time Media Library](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/), and the [Graph calling SDK](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/articles/index.html#graph-calling-sdk-and-stateful-client-builder) helps you build rich, real-time media, and calling bots.</span></span> <span data-ttu-id="a0d09-177">アプリケーションによりホストされるボットは、Windows 環境でホストされる必要があります。</span><span class="sxs-lookup"><span data-stu-id="a0d09-177">An application-hosted bot must be hosted in a Windows environment.</span></span> <span data-ttu-id="a0d09-178">詳細については、「アプリケーションホスト [型メディア ボット」を参照してください](./requirements-considerations-application-hosted-media-bots.md)。</span><span class="sxs-lookup"><span data-stu-id="a0d09-178">For more information, see [application-hosted media bots](./requirements-considerations-application-hosted-media-bots.md).</span></span>

## <a name="code-sample"></a><span data-ttu-id="a0d09-179">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="a0d09-179">Code sample</span></span>

| <span data-ttu-id="a0d09-180">**サンプル名**</span><span class="sxs-lookup"><span data-stu-id="a0d09-180">**Sample name**</span></span> | <span data-ttu-id="a0d09-181">**説明**</span><span class="sxs-lookup"><span data-stu-id="a0d09-181">**Description**</span></span> | <span data-ttu-id="a0d09-182">**Graph**</span><span class="sxs-lookup"><span data-stu-id="a0d09-182">**Graph**</span></span> |
|---------------|----------|--------|
| <span data-ttu-id="a0d09-183">Graph通信</span><span class="sxs-lookup"><span data-stu-id="a0d09-183">Graph communication</span></span> | <span data-ttu-id="a0d09-184">Graph Microsoft の通信プラットフォームとやり取りするための通信を提供します。</span><span class="sxs-lookup"><span data-stu-id="a0d09-184">Graph communications to interact with Microsoft's communications platform.</span></span> | [<span data-ttu-id="a0d09-185">View</span><span class="sxs-lookup"><span data-stu-id="a0d09-185">View</span></span>](https://github.com/microsoftgraph/microsoft-graph-comms-samples) |

## <a name="see-also"></a><span data-ttu-id="a0d09-186">関連項目</span><span class="sxs-lookup"><span data-stu-id="a0d09-186">See also</span></span>

- [<span data-ttu-id="a0d09-187">GraphAPI リファレンス</span><span class="sxs-lookup"><span data-stu-id="a0d09-187">Graph API reference</span></span>](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)

- [<span data-ttu-id="a0d09-188">サンプル アプリ</span><span class="sxs-lookup"><span data-stu-id="a0d09-188">Sample apps</span></span>](https://github.com/microsoftgraph/microsoft-graph-comms-samples)

- [<span data-ttu-id="a0d09-189">通話とオンライン会議をサポートするボットの登録</span><span class="sxs-lookup"><span data-stu-id="a0d09-189">Registering a bot that supports calls and online meetings</span></span>](./registering-calling-bot.md)

- [<span data-ttu-id="a0d09-190">Graphおよびオンライン会議ボットのアクセス許可の設定</span><span class="sxs-lookup"><span data-stu-id="a0d09-190">Graph permissions for calls and online meetings bots</span></span>](./registering-calling-bot.md#add-graph-permissions)

- [<span data-ttu-id="a0d09-191">コンピューターで通話とオンライン会議ボットを開発する方法</span><span class="sxs-lookup"><span data-stu-id="a0d09-191">How to develop calling and online meeting bots on your computer</span></span>](./debugging-local-testing-calling-meeting-bots.md)

- [<span data-ttu-id="a0d09-192">アプリケーションホスト型メディア ボットの要件と考慮事項</span><span class="sxs-lookup"><span data-stu-id="a0d09-192">Requirements and considerations for application-hosted media bots</span></span>](./requirements-considerations-application-hosted-media-bots.md)

- [<span data-ttu-id="a0d09-193">着信通知の処理に関する技術情報</span><span class="sxs-lookup"><span data-stu-id="a0d09-193">Technical information on handling incoming call notifications</span></span>](./call-notifications.md)

## <a name="next-step"></a><span data-ttu-id="a0d09-194">次の手順</span><span class="sxs-lookup"><span data-stu-id="a0d09-194">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a0d09-195">リアルタイムのメディア通話と会議</span><span class="sxs-lookup"><span data-stu-id="a0d09-195">Real-time media calls and meetings</span></span>](~/bots/calls-and-meetings/real-time-media-concepts.md)
