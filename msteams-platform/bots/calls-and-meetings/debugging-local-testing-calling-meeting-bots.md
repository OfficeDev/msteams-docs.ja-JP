---
title: ローカルで呼び出しや会議用ボットのデバッグを行う
description: ngrok を使用して、ローカル PC で通話やオンライン会議ボットを開発する方法について学習します。
ms.topic: how-to
keywords: ローカル開発 ngrok トンネル
ms.date: 11/18/2018
ms.openlocfilehash: e9b77df18c8d80f02134dc7912b5796023082039
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014307"
---
# <a name="how-to-develop-calling-and-online-meeting-bots-on-your-local-pc"></a><span data-ttu-id="4b284-104">ローカル PC で通話ボットとオンライン会議ボットを開発する方法</span><span class="sxs-lookup"><span data-stu-id="4b284-104">How to develop calling and online meeting bots on your local PC</span></span>

<span data-ttu-id="4b284-105">アプリ[の実行とデバッグでは](../../concepts/build-and-test/debug.md)[、ngrok](https://ngrok.com)を使用してローカル コンピューターとインターネットの間にトンネルを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="4b284-105">In [Run and debug your app](../../concepts/build-and-test/debug.md) we explain how to use [ngrok](https://ngrok.com) to create a tunnel between your local computer and the internet.</span></span> <span data-ttu-id="4b284-106">このトピックでは、ngrok とローカル PC を使用して、通話やオンライン会議をサポートするボットを開発する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="4b284-106">In this topic, learn how you can also use ngrok and your local PC to develop bots that support calls and online meetings.</span></span>

<span data-ttu-id="4b284-107">メッセージング ボットは HTTP を使用しますが、通話ボットとオンライン会議ボットは下位レベルの TCP を使用します。</span><span class="sxs-lookup"><span data-stu-id="4b284-107">Messaging bots use HTTP, but calls and online meeting bots use the lower-level TCP.</span></span> <span data-ttu-id="4b284-108">Ngrok は、HTTP トンネルに加えて TCP トンネルもサポートしています。その方法については、以下を参照してください。</span><span class="sxs-lookup"><span data-stu-id="4b284-108">Ngrok supports TCP tunnels in addition to HTTP tunnels; you'll learn how, below.</span></span>

## <a name="configuring-ngrokyml"></a><span data-ttu-id="4b284-109">ngrok.yml の構成</span><span class="sxs-lookup"><span data-stu-id="4b284-109">Configuring ngrok.yml</span></span>

<span data-ttu-id="4b284-110">[ngrok に移動し](https://ngrok.com)、無料アカウントにサインアップするか、既存のアカウントにログインします。</span><span class="sxs-lookup"><span data-stu-id="4b284-110">Go to [ngrok](https://ngrok.com) and sign up for a free account or log into your existing account.</span></span> <span data-ttu-id="4b284-111">ログインしたら、ダッシュボードに [移動して](https://dashboard.ngrok.com) 、authtoken を取得します。</span><span class="sxs-lookup"><span data-stu-id="4b284-111">Once you've logged in, go to the [dashboard](https://dashboard.ngrok.com) and get your authtoken.</span></span>

<span data-ttu-id="4b284-112">ngrok 構成ファイルを作成し (このファイルの場所の詳細については、このファイルを参照 `ngrok.yml` してください)、次の行を追加します。 [](https://ngrok.com/docs#config)</span><span class="sxs-lookup"><span data-stu-id="4b284-112">Create an ngrok configuration file `ngrok.yml` (see [here](https://ngrok.com/docs#config) for more information on where this file can be located) and add this line:</span></span>

  `authtoken: <Your-AuthToken>`

## <a name="setting-up-signaling"></a><span data-ttu-id="4b284-113">シグナリングの設定</span><span class="sxs-lookup"><span data-stu-id="4b284-113">Setting up signaling</span></span>

<span data-ttu-id="4b284-114">通話 [とオンライン会議](./calls-meetings-bots-overview.md)のボットでは、通話信号について説明しました。ボットが通話中に新しい通話やイベントを検出して応答する方法について説明しました。</span><span class="sxs-lookup"><span data-stu-id="4b284-114">In [Calls and online meetings bots](./calls-meetings-bots-overview.md), we discussed call signaling — how bots detect and respond to new calls and events during a call.</span></span> <span data-ttu-id="4b284-115">呼び出し信号イベントは、HTTP POST を介してボットの呼び出しエンドポイントに送信されます。</span><span class="sxs-lookup"><span data-stu-id="4b284-115">Call signaling events are sent via HTTP POST to the bot's calling endpoint.</span></span>

<span data-ttu-id="4b284-116">ボットのメッセージング API と同様に、リアルタイム メディア プラットフォームがボットと通信するには、ボットがインターネット上で到達可能である必要があります。</span><span class="sxs-lookup"><span data-stu-id="4b284-116">As with the bot's messaging API, in order for the Real-time Media Platform to talk to your bot, your bot must be reachable over the internet.</span></span> <span data-ttu-id="4b284-117">Ngrok を使用すると、この操作が簡単になります。ngrok.yml に次の行を追加します。</span><span class="sxs-lookup"><span data-stu-id="4b284-117">Ngrok makes this simple — add the following lines to your ngrok.yml:</span></span>

```yaml
tunnels:
    signaling:
        addr: 12345
        proto: http
```

## <a name="setting-up-local-media"></a><span data-ttu-id="4b284-118">ローカル メディアの設定</span><span class="sxs-lookup"><span data-stu-id="4b284-118">Setting up local media</span></span>

> [!NOTE]
> <span data-ttu-id="4b284-119">このセクションは、アプリケーションホスト型メディア ボットでのみ必要であり、メディアを自分でホストしない場合はスキップできます。</span><span class="sxs-lookup"><span data-stu-id="4b284-119">This section is only required for application-hosted media bots and can be skipped if you don't host media yourself.</span></span>

<span data-ttu-id="4b284-120">アプリケーションホスト型メディアは、証明書と TCP トンネルを使用します。</span><span class="sxs-lookup"><span data-stu-id="4b284-120">Application-hosted media uses certificates and TCP tunnels.</span></span> <span data-ttu-id="4b284-121">次の手順が必要です。</span><span class="sxs-lookup"><span data-stu-id="4b284-121">The following steps are required:</span></span>

- <span data-ttu-id="4b284-122">Ngrok のパブリック TCP エンドポイントの URL は固定されています。</span><span class="sxs-lookup"><span data-stu-id="4b284-122">Ngrok's public TCP endpoints have fixed URLs.</span></span> <span data-ttu-id="4b284-123">これらは `0.tcp.ngrok.io` 、 `1.tcp.ngrok.io` 次の場合などです。</span><span class="sxs-lookup"><span data-stu-id="4b284-123">They are `0.tcp.ngrok.io`, `1.tcp.ngrok.io`, and so on.</span></span> <span data-ttu-id="4b284-124">これらの URL をポイントするサービスの DNS CNAME エントリが必要です。</span><span class="sxs-lookup"><span data-stu-id="4b284-124">You should have a DNS CNAME entry for your service that points to these URLs.</span></span> <span data-ttu-id="4b284-125">この例では、参照、参照、など `0.bot.contoso.com` `0.tcp.ngrok.io` `1.bot.contoso.com` `1.tcp.ngrok.io` とします。</span><span class="sxs-lookup"><span data-stu-id="4b284-125">In this example, let's say `0.bot.contoso.com` refers to `0.tcp.ngrok.io`, `1.bot.contoso.com` refers to `1.tcp.ngrok.io`, and so on.</span></span>
- <span data-ttu-id="4b284-126">URL には SSL 証明書が必要です。</span><span class="sxs-lookup"><span data-stu-id="4b284-126">A SSL certificate is required for your URLs.</span></span> <span data-ttu-id="4b284-127">簡単に実行するには、ワイルドカード ドメインに発行された SSL 証明書を使用します。</span><span class="sxs-lookup"><span data-stu-id="4b284-127">To make it easy, use a SSL certificate issued to a wild card domain.</span></span> <span data-ttu-id="4b284-128">この場合は、 `*.bot.contoso.com` .</span><span class="sxs-lookup"><span data-stu-id="4b284-128">In this case, it would be `*.bot.contoso.com`.</span></span> <span data-ttu-id="4b284-129">この SSL 証明書はメディア SDK によって検証されます。そのため、ボットのパブリック URL と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4b284-129">This SSL certificate is validated by the media SDK, so it should match your bot's public URL.</span></span> <span data-ttu-id="4b284-130">拇印をメモし、コンピューターの証明書にインストールします。</span><span class="sxs-lookup"><span data-stu-id="4b284-130">Note the thumbprint and install it in your machine certificates.</span></span>
- <span data-ttu-id="4b284-131">次に、トラフィックを localhost に転送する TCP トンネルをセットアップします。</span><span class="sxs-lookup"><span data-stu-id="4b284-131">Now, setup a TCP tunnel to forward the traffic to localhost.</span></span> <span data-ttu-id="4b284-132">ngrok.yml に次の行を記述します。</span><span class="sxs-lookup"><span data-stu-id="4b284-132">Write the following lines into your ngrok.yml:</span></span>

    ```yaml
    media:
        addr: 8445
        proto: tcp
    ```

## <a name="start-ngrok"></a><span data-ttu-id="4b284-133">ngrok を起動する</span><span class="sxs-lookup"><span data-stu-id="4b284-133">Start ngrok</span></span>

<span data-ttu-id="4b284-134">ngrok 構成の準備が整ったので、次の方法で起動します。</span><span class="sxs-lookup"><span data-stu-id="4b284-134">Now that the ngrok configuration is ready, launch it:</span></span>

  `ngrok.exe start -all -config <Path to your ngrok.yml>`

<span data-ttu-id="4b284-135">これにより ngrok が開始され、localhost へのトンネルを提供するパブリック URL が定義されます。</span><span class="sxs-lookup"><span data-stu-id="4b284-135">This starts ngrok and defines the public URLs which provide the tunnels to your localhost.</span></span> <span data-ttu-id="4b284-136">出力は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="4b284-136">The output looks like the following:</span></span>

```cmd
Forwarding  http://signal.ngrok.io -> localhost:12345
Forwarding  https://signal.ngrok.io -> localhost:12345
Forwarding  tcp://1.tcp.ngrok.io:12332 -> localhost:8445
```

<span data-ttu-id="4b284-137">次に示すのは、信号ポートであり、アプリケーションでホストされるポートであり、ngrok によって公開されるリモート メディア `12345` `8445` `12332` ポートです。</span><span class="sxs-lookup"><span data-stu-id="4b284-137">Here, `12345` is the signaling port, `8445` is the application-hosted port, and `12332` is the remote media port exposed by ngrok.</span></span> <span data-ttu-id="4b284-138">転送先が設定されている点に注意 `1.bot.contoso.com` してください `1.tcp.ngrok.io` 。</span><span class="sxs-lookup"><span data-stu-id="4b284-138">Note that we have a forwarding from `1.bot.contoso.com` to `1.tcp.ngrok.io`.</span></span> <span data-ttu-id="4b284-139">これは、ボットのメディア URL として使用されます。</span><span class="sxs-lookup"><span data-stu-id="4b284-139">This will be used as the media URL for the bot.</span></span> <span data-ttu-id="4b284-140">もちろん、これらのポート番号は単なる例であり、使用可能な任意のポートを使用できます。</span><span class="sxs-lookup"><span data-stu-id="4b284-140">Of course, these port numbers are just examples and you can use any available port.</span></span>

### <a name="update-code"></a><span data-ttu-id="4b284-141">コードを更新する</span><span class="sxs-lookup"><span data-stu-id="4b284-141">Update code</span></span>

<span data-ttu-id="4b284-142">ngrok が稼働したら、設定した構成を使用するコードを更新します。</span><span class="sxs-lookup"><span data-stu-id="4b284-142">Once ngrok is up and running, update the code to use the config you just set up.</span></span>

#### <a name="update-signaling"></a><span data-ttu-id="4b284-143">更新信号</span><span class="sxs-lookup"><span data-stu-id="4b284-143">Update signaling</span></span>

- <span data-ttu-id="4b284-144">BotBuilder 呼び出しで `NotificationUrl` 、ngrok によって提供される信号 URL に変更します。</span><span class="sxs-lookup"><span data-stu-id="4b284-144">In the BotBuilder call, change the `NotificationUrl` to the signaling URL provided by ngrok.</span></span>

```csharp
statefulClientBuilder.SetNotificationUrl(
    new Uri("https://signal.ngrok.io/notificationEndpoint"))
```

> [!NOTE]
> <span data-ttu-id="4b284-145">信号を ngrok によって提供される信号に置き換え、通知を受け取るコントローラー パス `NotificationEndpoint` に置き換える。</span><span class="sxs-lookup"><span data-stu-id="4b284-145">Replace signal with the one provided by ngrok and the `NotificationEndpoint` with the controller path that receives notification.</span></span>

> <span data-ttu-id="4b284-146">**重要**: URL は HTTPS `SetNotificationUrl` である必要があります。</span><span class="sxs-lookup"><span data-stu-id="4b284-146">**IMPORTANT**: The URL in `SetNotificationUrl` must be HTTPS.</span></span>

> <span data-ttu-id="4b284-147">**重要**: ローカル インスタンスは信号ポートで HTTP トラフィックをリッスンしている必要があります。</span><span class="sxs-lookup"><span data-stu-id="4b284-147">**IMPORTANT**: Your local instance must be listening to HTTP traffic on the signaling port.</span></span> <span data-ttu-id="4b284-148">通話およびオンライン会議プラットフォームによって行われた要求は、エンド to エンドの暗号化が設定されていない限り、localhost HTTP トラフィックとしてボットに到達します。</span><span class="sxs-lookup"><span data-stu-id="4b284-148">The requests made by the calls and online meetings platform will reach the bot as localhost HTTP traffic unless end-to-end encryption is set up.</span></span>

#### <a name="update-media"></a><span data-ttu-id="4b284-149">メディアを更新する</span><span class="sxs-lookup"><span data-stu-id="4b284-149">Update media</span></span>

<span data-ttu-id="4b284-150">次の `MediaPlatformSettings` 手順に従って更新します。</span><span class="sxs-lookup"><span data-stu-id="4b284-150">Update your `MediaPlatformSettings` to the following.</span></span>

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
> <span data-ttu-id="4b284-151">上記の証明書の拇印は、サービスの FQDN と一致している必要があります。</span><span class="sxs-lookup"><span data-stu-id="4b284-151">The certificate thumbprint provided above should match the Service FQDN.</span></span> <span data-ttu-id="4b284-152">DNS エントリが必要になるのは、この理由です。</span><span class="sxs-lookup"><span data-stu-id="4b284-152">That is why the DNS entries are required.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4b284-153">次の手順</span><span class="sxs-lookup"><span data-stu-id="4b284-153">Next steps</span></span>

<span data-ttu-id="4b284-154">ボットをローカルで実行し、すべてのフローが localhost から機能する。</span><span class="sxs-lookup"><span data-stu-id="4b284-154">Your bot can now run locally and all the flows work from your localhost.</span></span>

## <a name="caveats"></a><span data-ttu-id="4b284-155">注意点</span><span class="sxs-lookup"><span data-stu-id="4b284-155">Caveats</span></span>

- <span data-ttu-id="4b284-156">Ngrok 無料アカウント **では、エンドツーエンド** の暗号化は提供しません。</span><span class="sxs-lookup"><span data-stu-id="4b284-156">Ngrok free accounts **don't** provide end-to-end encryption.</span></span> <span data-ttu-id="4b284-157">HTTPS データは ngrok URL で終わり、データフローは ngrok から暗号化されません `localhost` 。</span><span class="sxs-lookup"><span data-stu-id="4b284-157">The HTTPS data ends at the ngrok URL and the data flows unencrypted from ngrok to `localhost`.</span></span> <span data-ttu-id="4b284-158">エンドツーエンドの暗号化が必要な場合は、有料の ngrok アカウントを検討してください。</span><span class="sxs-lookup"><span data-stu-id="4b284-158">If you require end-to-end encryption, consider a paid ngrok account.</span></span> <span data-ttu-id="4b284-159">セキュリティ [で保護されたエンド](https://ngrok.com/docs#tls) エンド トンネルを設定する手順については、「TLS トンネル」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="4b284-159">See [TLS tunnels](https://ngrok.com/docs#tls) for steps on setting up secure end-to-end tunnels.</span></span>
- <span data-ttu-id="4b284-160">ボットコールバック URL は動的なので、着信呼び出しのシナリオでは、ngrok エンドポイントを頻繁に更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4b284-160">Because the bot callback URL is dynamic, incoming call scenarios require you to frequently update your ngrok endpoints.</span></span> <span data-ttu-id="4b284-161">これを修正する 1 つの方法は、ボットとプラットフォームを指し示す固定サブドメインを提供する有料の ngrok アカウントを使用する方法です。</span><span class="sxs-lookup"><span data-stu-id="4b284-161">One way to fix this is to use a paid ngrok account which provides fixed subdomains to which you can point your bot and the platform.</span></span>
- <span data-ttu-id="4b284-162">Ngrok トンネルは Azure Service Fabric でも [使用できます](/azure/service-fabric/service-fabric-overview)。</span><span class="sxs-lookup"><span data-stu-id="4b284-162">Ngrok tunnels can also be used with [Azure Service Fabric](/azure/service-fabric/service-fabric-overview).</span></span> <span data-ttu-id="4b284-163">これを行う方法の例については、HueBot サンプル アプリ [をご覧ください](/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/LocalMediaSamples/HueBot/HueBot)。</span><span class="sxs-lookup"><span data-stu-id="4b284-163">For an example of how to do this, see the [HueBot sample app](/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/LocalMediaSamples/HueBot/HueBot).</span></span>
