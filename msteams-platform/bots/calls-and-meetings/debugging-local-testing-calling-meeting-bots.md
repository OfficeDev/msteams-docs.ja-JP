---
title: ローカルで呼び出しや会議用ボットのデバッグを行う
description: ngrok を使用して、ローカル PC で通話とオンライン会議ボットを開発する方法について学習します。
ms.topic: how-to
localization_priority: Normal
keywords: ローカル開発 ngrok トンネル
ms.date: 11/18/2018
ms.openlocfilehash: 0f29f77e5030a7dbef9e8f7cefae4e055b7cc5b5
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020163"
---
# <a name="develop-calling-and-online-meeting-bots-on-your-local-pc"></a><span data-ttu-id="c88c5-104">ローカル PC で通話およびオンライン会議ボットを開発する</span><span class="sxs-lookup"><span data-stu-id="c88c5-104">Develop calling and online meeting bots on your local PC</span></span>

<span data-ttu-id="c88c5-105">[ [アプリの実行とデバッグ](../../concepts/build-and-test/debug.md) ] では [、ngrok](https://ngrok.com) を使用してローカル コンピューターとインターネットの間にトンネルを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="c88c5-105">In [Run and debug your app](../../concepts/build-and-test/debug.md) we explain how to use [ngrok](https://ngrok.com) to create a tunnel between your local computer and the internet.</span></span> <span data-ttu-id="c88c5-106">このトピックでは、ngrok とローカル PC を使用して、通話やオンライン会議をサポートするボットを開発する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="c88c5-106">In this topic, learn how you can also use ngrok and your local PC to develop bots that support calls and online meetings.</span></span>

<span data-ttu-id="c88c5-107">メッセージング ボットは HTTP を使用しますが、通話とオンライン会議ボットは下位レベルの TCP を使用します。</span><span class="sxs-lookup"><span data-stu-id="c88c5-107">Messaging bots use HTTP, but calls and online meeting bots use the lower-level TCP.</span></span> <span data-ttu-id="c88c5-108">Ngrok は、HTTP トンネルに加えて TCP トンネルもサポートします。</span><span class="sxs-lookup"><span data-stu-id="c88c5-108">Ngrok supports TCP tunnels in addition to HTTP tunnels.</span></span> 

## <a name="configure-ngrokyml"></a><span data-ttu-id="c88c5-109">ngrok.yml を構成する</span><span class="sxs-lookup"><span data-stu-id="c88c5-109">Configure ngrok.yml</span></span>

<span data-ttu-id="c88c5-110">[ngrok に移動し](https://ngrok.com)、無料アカウントにサインアップするか、既存のアカウントにログインします。</span><span class="sxs-lookup"><span data-stu-id="c88c5-110">Go to [ngrok](https://ngrok.com) and sign up for a free account or log into your existing account.</span></span> <span data-ttu-id="c88c5-111">サインインした後、ダッシュボードに [移動し、](https://dashboard.ngrok.com) 認証トークンを取得します。</span><span class="sxs-lookup"><span data-stu-id="c88c5-111">After you've signed in, go to the [dashboard](https://dashboard.ngrok.com) and get your auth token.</span></span>

<span data-ttu-id="c88c5-112">ngrok 構成ファイルを作成し `ngrok.yml` 、次の行を追加します。</span><span class="sxs-lookup"><span data-stu-id="c88c5-112">Create an ngrok configuration file `ngrok.yml` and add the following line.</span></span> <span data-ttu-id="c88c5-113">ファイルの場所の詳細については [、「ngrok」を参照してください](https://ngrok.com/docs#config)。</span><span class="sxs-lookup"><span data-stu-id="c88c5-113">For more information on where the file can be located, see [ngrok](https://ngrok.com/docs#config):</span></span>

  `authtoken: <Your-AuthToken>`

## <a name="set-up-signaling"></a><span data-ttu-id="c88c5-114">シグナリングのセットアップ</span><span class="sxs-lookup"><span data-stu-id="c88c5-114">Set up signaling</span></span>

<span data-ttu-id="c88c5-115">[ [通話とオンライン会議の](./calls-meetings-bots-overview.md)ボット] では、ボットが通話中に新しい通話やイベントを検出して応答する方法について、通話シグナリングについて説明しました。</span><span class="sxs-lookup"><span data-stu-id="c88c5-115">In [Calls and online meetings bots](./calls-meetings-bots-overview.md), we discussed call signaling on how bots detect and respond to new calls and events during a call.</span></span> <span data-ttu-id="c88c5-116">呼び出しシグナル イベントは、HTTP POST を介してボットの呼び出しエンドポイントに送信されます。</span><span class="sxs-lookup"><span data-stu-id="c88c5-116">Call signaling events are sent through HTTP POST to the bot's calling endpoint.</span></span>

<span data-ttu-id="c88c5-117">ボットのメッセージング API と同様に、リアルタイム メディア プラットフォームがボットと通信するには、ボットがインターネット上で到達可能である必要があります。</span><span class="sxs-lookup"><span data-stu-id="c88c5-117">As with the bot's messaging API, for the Real-time Media Platform to talk to your bot, your bot must be reachable over the internet.</span></span> <span data-ttu-id="c88c5-118">Ngrok は、この単純な操作を行います。</span><span class="sxs-lookup"><span data-stu-id="c88c5-118">Ngrok makes this simple.</span></span> <span data-ttu-id="c88c5-119">ngrok.yml に次の行を追加します。</span><span class="sxs-lookup"><span data-stu-id="c88c5-119">Add the following lines to your ngrok.yml:</span></span>

```yaml
tunnels:
    signaling:
        addr: 12345
        proto: http
```

## <a name="set-up-local-media"></a><span data-ttu-id="c88c5-120">ローカル メディアのセットアップ</span><span class="sxs-lookup"><span data-stu-id="c88c5-120">Set up local media</span></span>

> [!NOTE]
> <span data-ttu-id="c88c5-121">このセクションは、アプリケーションホスト型メディア ボットでのみ必要であり、自分でメディアをホストしない場合はスキップできます。</span><span class="sxs-lookup"><span data-stu-id="c88c5-121">This section is only required for application-hosted media bots and can be skipped if you don't host media yourself.</span></span>

<span data-ttu-id="c88c5-122">アプリケーションホスト型メディアは、証明書と TCP トンネルを使用します。</span><span class="sxs-lookup"><span data-stu-id="c88c5-122">Application-hosted media uses certificates and TCP tunnels.</span></span> <span data-ttu-id="c88c5-123">以下の手順が必要です。</span><span class="sxs-lookup"><span data-stu-id="c88c5-123">The following steps are required:</span></span>

1. <span data-ttu-id="c88c5-124">Ngrok のパブリック TCP エンドポイントには固定 URL があります。</span><span class="sxs-lookup"><span data-stu-id="c88c5-124">Ngrok's public TCP endpoints have fixed URLs.</span></span> <span data-ttu-id="c88c5-125">これらは `0.tcp.ngrok.io` `1.tcp.ngrok.io` 、、、などです。</span><span class="sxs-lookup"><span data-stu-id="c88c5-125">They are `0.tcp.ngrok.io`, `1.tcp.ngrok.io`, and so on.</span></span> <span data-ttu-id="c88c5-126">これらの URL をポイントするサービスの DNS CNAME エントリが必要です。</span><span class="sxs-lookup"><span data-stu-id="c88c5-126">You must have a DNS CNAME entry for your service that points to these URLs.</span></span> <span data-ttu-id="c88c5-127">たとえば、参照、参照、などと `0.bot.contoso.com` `0.tcp.ngrok.io` `1.bot.contoso.com` `1.tcp.ngrok.io` します。</span><span class="sxs-lookup"><span data-stu-id="c88c5-127">For example, let's say `0.bot.contoso.com` refers to `0.tcp.ngrok.io`, `1.bot.contoso.com` refers to `1.tcp.ngrok.io`, and so on.</span></span>
2. <span data-ttu-id="c88c5-128">URL には SSL 証明書が必要です。</span><span class="sxs-lookup"><span data-stu-id="c88c5-128">An SSL certificate is required for your URLs.</span></span> <span data-ttu-id="c88c5-129">簡単に行う場合は、ワイルドカード ドメインに発行された SSL 証明書を使用します。</span><span class="sxs-lookup"><span data-stu-id="c88c5-129">To make it easy, use an SSL certificate issued to a wild card domain.</span></span> <span data-ttu-id="c88c5-130">この場合は、 `*.bot.contoso.com` です。</span><span class="sxs-lookup"><span data-stu-id="c88c5-130">In this case, it would be `*.bot.contoso.com`.</span></span> <span data-ttu-id="c88c5-131">この SSL 証明書はメディア SDK によって検証されます。そのため、ボットのパブリック URL と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c88c5-131">This SSL certificate is validated by the media SDK, so it must match your bot's public URL.</span></span> <span data-ttu-id="c88c5-132">拇印をメモし、コンピューター証明書にインストールします。</span><span class="sxs-lookup"><span data-stu-id="c88c5-132">Note the thumbprint and install it in your machine certificates.</span></span>
3. <span data-ttu-id="c88c5-133">次に、トラフィックを localhost に転送する TCP トンネルを設定します。</span><span class="sxs-lookup"><span data-stu-id="c88c5-133">Now, set up a TCP tunnel to forward the traffic to localhost.</span></span> <span data-ttu-id="c88c5-134">ngrok.yml に次の行を記述します。</span><span class="sxs-lookup"><span data-stu-id="c88c5-134">Write the following lines into your ngrok.yml:</span></span>

    ```yaml
    media:
        addr: 8445
        proto: tcp
    ```

## <a name="start-ngrok"></a><span data-ttu-id="c88c5-135">ngrok を開始する</span><span class="sxs-lookup"><span data-stu-id="c88c5-135">Start ngrok</span></span>

<span data-ttu-id="c88c5-136">ngrok 構成の準備が整ったので、次の方法で起動します。</span><span class="sxs-lookup"><span data-stu-id="c88c5-136">Now that the ngrok configuration is ready, launch it:</span></span>

  `ngrok.exe start -all -config <Path to your ngrok.yml>`

<span data-ttu-id="c88c5-137">これは ngrok を開始し、ローカル ホストへのトンネルを提供するパブリック URL を定義します。</span><span class="sxs-lookup"><span data-stu-id="c88c5-137">This starts ngrok and defines the public URLs which provide the tunnels to your localhost.</span></span> <span data-ttu-id="c88c5-138">出力の例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="c88c5-138">Following is an example of the output:</span></span>

```cmd
Forwarding  http://signal.ngrok.io -> localhost:12345
Forwarding  https://signal.ngrok.io -> localhost:12345
Forwarding  tcp://1.tcp.ngrok.io:12332 -> localhost:8445
```

<span data-ttu-id="c88c5-139">ここでは、シグナリング ポート、アプリケーションホストポート、および ngrok によって公開される `12345` リモート メディア `8445` `12332` ポートを示します。</span><span class="sxs-lookup"><span data-stu-id="c88c5-139">Here, `12345` is the signaling port, `8445` is the application-hosted port, and `12332` is the remote media port exposed by ngrok.</span></span> <span data-ttu-id="c88c5-140">からへの転送があります `1.bot.contoso.com` `1.tcp.ngrok.io` 。</span><span class="sxs-lookup"><span data-stu-id="c88c5-140">Note that we have a forwarding from `1.bot.contoso.com` to `1.tcp.ngrok.io`.</span></span> <span data-ttu-id="c88c5-141">これは、ボットのメディア URL として使用されます。</span><span class="sxs-lookup"><span data-stu-id="c88c5-141">This will be used as the media URL for the bot.</span></span> <span data-ttu-id="c88c5-142">もちろん、これらのポート番号は単なる例であり、使用可能な任意のポートを使用できます。</span><span class="sxs-lookup"><span data-stu-id="c88c5-142">Of course, these port numbers are just examples and you can use any available port.</span></span>

### <a name="update-code"></a><span data-ttu-id="c88c5-143">コードを更新する</span><span class="sxs-lookup"><span data-stu-id="c88c5-143">Update code</span></span>

<span data-ttu-id="c88c5-144">ngrok が稼働した後、セットアップした構成を使用するコードを更新します。</span><span class="sxs-lookup"><span data-stu-id="c88c5-144">After ngrok is up and running, update the code to use the config you just set up.</span></span>

#### <a name="update-signaling"></a><span data-ttu-id="c88c5-145">信号の更新</span><span class="sxs-lookup"><span data-stu-id="c88c5-145">Update signaling</span></span>

<span data-ttu-id="c88c5-146">BotBuilder 呼び出しで `NotificationUrl` 、ngrok によって提供されるシグナリング URL に変更します。</span><span class="sxs-lookup"><span data-stu-id="c88c5-146">In the BotBuilder call, change the `NotificationUrl` to the signaling URL provided by ngrok.</span></span>

```csharp
statefulClientBuilder.SetNotificationUrl(
    new Uri("https://signal.ngrok.io/notificationEndpoint"))
```

> [!NOTE]
> <span data-ttu-id="c88c5-147">信号を ngrok が提供するパスに置き換え、通知を受け取る `NotificationEndpoint` コントローラー パスに置き換える。</span><span class="sxs-lookup"><span data-stu-id="c88c5-147">Replace signal with the one provided by ngrok and the `NotificationEndpoint` with the controller path that receives notification.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="c88c5-148">URL は HTTPS `SetNotificationUrl` である必要があります。</span><span class="sxs-lookup"><span data-stu-id="c88c5-148">The URL in `SetNotificationUrl` must be HTTPS.</span></span>
> 
> <span data-ttu-id="c88c5-149">ローカル インスタンスは、シグナリング ポートで HTTP トラフィックをリッスンしている必要があります。</span><span class="sxs-lookup"><span data-stu-id="c88c5-149">Your local instance must be listening to HTTP traffic on the signaling port.</span></span> <span data-ttu-id="c88c5-150">通話とオンライン会議プラットフォームによって行われた要求は、エンドツーエンドの暗号化が設定されていない限り、ボットに localhost HTTP トラフィックとして到達します。</span><span class="sxs-lookup"><span data-stu-id="c88c5-150">The requests made by the calls and online meetings platform will reach the bot as localhost HTTP traffic unless end-to-end encryption is set up.</span></span>

#### <a name="update-media"></a><span data-ttu-id="c88c5-151">メディアの更新</span><span class="sxs-lookup"><span data-stu-id="c88c5-151">Update media</span></span>

<span data-ttu-id="c88c5-152">次のように `MediaPlatformSettings` 更新します。</span><span class="sxs-lookup"><span data-stu-id="c88c5-152">Update your `MediaPlatformSettings` as following:</span></span>

```csharp
var mediaPlatform = new MediaPlatformSettings
{
    ApplicationId = <Your application id>
    MediaPlatformInstanceSettings = new MediaPlatformInstanceSettings
    {
        CertificateThumbprint = <Your SSL Cert thumbprint>,
        InstanceInternalPort = <Localhost media port>,
        InstancePublicPort = <Ngrok exposed remote media port>,
        InstancePublicIPAddress = new IPAddress(0x0),
        ServiceFqdn = <Media url for bot (eg: 1.bot.contoso.com)>,
    },
}
```

> [!NOTE]
> <span data-ttu-id="c88c5-153">で提供される証明書の拇印は `MediaPlatformSettings` 、サービス FQDN と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c88c5-153">The certificate thumbprint provided in the `MediaPlatformSettings` must match the Service FQDN.</span></span> <span data-ttu-id="c88c5-154">DNS エントリが必要な理由です。</span><span class="sxs-lookup"><span data-stu-id="c88c5-154">That is why the DNS entries are required.</span></span>

## <a name="caveats"></a><span data-ttu-id="c88c5-155">注意点</span><span class="sxs-lookup"><span data-stu-id="c88c5-155">Caveats</span></span>

- <span data-ttu-id="c88c5-156">Ngrok 無料アカウント **は、エンドツーエンド** の暗号化を提供しません。</span><span class="sxs-lookup"><span data-stu-id="c88c5-156">Ngrok free accounts **don't** provide end-to-end encryption.</span></span> <span data-ttu-id="c88c5-157">HTTPS データは ngrok URL で終了し、データ フローは ngrok から . `localhost`</span><span class="sxs-lookup"><span data-stu-id="c88c5-157">The HTTPS data ends at the ngrok URL and the data flows unencrypted from ngrok to `localhost`.</span></span> <span data-ttu-id="c88c5-158">エンドツーエンドの暗号化が必要な場合は、有料の ngrok アカウントを検討してください。</span><span class="sxs-lookup"><span data-stu-id="c88c5-158">If you require end-to-end encryption, consider a paid ngrok account.</span></span> <span data-ttu-id="c88c5-159">セキュリティ [で保護されたエンドツーエンド トンネル](https://ngrok.com/docs#tls) をセットアップする手順については、「TLS トンネル」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c88c5-159">See [TLS tunnels](https://ngrok.com/docs#tls) for steps on setting up secure end-to-end tunnels.</span></span>
- <span data-ttu-id="c88c5-160">ボットコールバック URL は動的なので、着信呼び出しのシナリオでは、ngrok エンドポイントを頻繁に更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c88c5-160">Because the bot callback URL is dynamic, incoming call scenarios require you to frequently update your ngrok endpoints.</span></span> <span data-ttu-id="c88c5-161">これを修正する 1 つの方法は、ボットとプラットフォームをポイントできる固定サブドメインを提供する有料の ngrok アカウントを使用する方法です。</span><span class="sxs-lookup"><span data-stu-id="c88c5-161">One way to fix this is to use a paid ngrok account which provides fixed subdomains to which you can point your bot and the platform.</span></span>
- <span data-ttu-id="c88c5-162">Ngrok トンネルは Azure Service [Fabric でも使用できます](/azure/service-fabric/service-fabric-overview)。</span><span class="sxs-lookup"><span data-stu-id="c88c5-162">Ngrok tunnels can also be used with [Azure Service Fabric](/azure/service-fabric/service-fabric-overview).</span></span> <span data-ttu-id="c88c5-163">これを行う方法の例については、「HueBot サンプル アプリ [」を参照してください](/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/LocalMediaSamples/HueBot/HueBot)。</span><span class="sxs-lookup"><span data-stu-id="c88c5-163">For an example of how to do this, see the [HueBot sample app](/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/LocalMediaSamples/HueBot/HueBot).</span></span>
