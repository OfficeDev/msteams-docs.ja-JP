---
title: ローカル PC で通話およびオンライン会議のボットを開発する方法
description: Ngrok を使用して、ローカル PC で通話やオンライン会議のボットを開発する方法についても説明します。
keywords: ローカル開発 ngrok トンネル
ms.date: 11/18/2018
ms.openlocfilehash: b6cd2ba5a3866da8085b3da42377ab9e21f12f5f
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675042"
---
# <a name="how-to-develop-calling-and-online-meeting-bots-on-your-local-pc"></a><span data-ttu-id="79936-104">ローカル PC で通話およびオンライン会議のボットを開発する方法</span><span class="sxs-lookup"><span data-stu-id="79936-104">How to develop calling and online meeting bots on your local PC</span></span>

<span data-ttu-id="79936-105">「[アプリの実行とデバッグ](../../concepts/build-and-test/debug.md)」では、 [ngrok](https://ngrok.com)を使用して、ローカルコンピューターとインターネットとの間のトンネルを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="79936-105">In [Run and debug your app](../../concepts/build-and-test/debug.md) we explain how to use [ngrok](https://ngrok.com) to create a tunnel between your local computer and the internet.</span></span> <span data-ttu-id="79936-106">このトピックでは、ngrok とローカル PC を使用して、通話とオンライン会議をサポートするボットを開発する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="79936-106">In this topic, learn how you can also use ngrok and your local PC to develop bots that support calls and online meetings.</span></span>

<span data-ttu-id="79936-107">メッセージングのボットは HTTP を使用しますが、呼び出しとオンライン会議のボットは下位レベルの TCP を使用します。</span><span class="sxs-lookup"><span data-stu-id="79936-107">Messaging bots use HTTP, but calls and online meeting bots use the lower-level TCP.</span></span> <span data-ttu-id="79936-108">Ngrok は、HTTP トンネルに加えて TCP トンネルもサポートします。詳細については、以下を参照してください。</span><span class="sxs-lookup"><span data-stu-id="79936-108">Ngrok supports TCP tunnels in addition to HTTP tunnels; you'll learn how, below.</span></span>

## <a name="configuring-ngrokyml"></a><span data-ttu-id="79936-109">Yml を構成する ngrok</span><span class="sxs-lookup"><span data-stu-id="79936-109">Configuring ngrok.yml</span></span>

<span data-ttu-id="79936-110">[Ngrok](https://ngrok.com)に移動し、無料のアカウントまたはログを既存のアカウントにサインアップします。</span><span class="sxs-lookup"><span data-stu-id="79936-110">Go to [ngrok](https://ngrok.com) and sign up for a free account or log into your existing account.</span></span> <span data-ttu-id="79936-111">ログインしたら、[ダッシュボード](https://dashboard.ngrok.com)に移動して authtoken を取得します。</span><span class="sxs-lookup"><span data-stu-id="79936-111">Once you've logged in, go to the [dashboard](https://dashboard.ngrok.com) and get your authtoken.</span></span>

<span data-ttu-id="79936-112">Ngrok 構成ファイル`ngrok.yml`を作成し (このファイルが保存されている場所の詳細について[は、こちら](https://ngrok.com/docs#config)を参照してください)、次の行を追加します。</span><span class="sxs-lookup"><span data-stu-id="79936-112">Create an ngrok configuration file `ngrok.yml` (see [here](https://ngrok.com/docs#config) for more information on where this file can be located) and add this line:</span></span>

  `authtoken: <Your-AuthToken>`

## <a name="setting-up-signaling"></a><span data-ttu-id="79936-113">信号の設定</span><span class="sxs-lookup"><span data-stu-id="79936-113">Setting up signaling</span></span>

<span data-ttu-id="79936-114">「[通話とオンライン会議のボット](./calls-meetings-bots-overview.md)」では、通話のシグナリングについて説明し、呼び出し中に新しい通話やイベントに対してボットが検出して応答する方法を説明しました。</span><span class="sxs-lookup"><span data-stu-id="79936-114">In [Calls and online meetings bots](./calls-meetings-bots-overview.md), we discussed call signaling — how bots detect and respond to new calls and events during a call.</span></span> <span data-ttu-id="79936-115">通話シグナリングイベントは、ボットの呼び出しエンドポイントに HTTP POST 経由で送信されます。</span><span class="sxs-lookup"><span data-stu-id="79936-115">Call signaling events are sent via HTTP POST to the bot's calling endpoint.</span></span>

<span data-ttu-id="79936-116">Bot のメッセージング API と同様に、リアルタイムメディアプラットフォームが bot と通信するためには、ボットがインターネットを介して到達可能である必要があります。</span><span class="sxs-lookup"><span data-stu-id="79936-116">As with the bot's messaging API, in order for the Real-time Media Platform to talk to your bot, your bot must be reachable over the internet.</span></span> <span data-ttu-id="79936-117">Ngrok は、次の行を Ngrok に追加します。</span><span class="sxs-lookup"><span data-stu-id="79936-117">Ngrok makes this simple — add the following lines to your ngrok.yml:</span></span>

```yaml
tunnels:
    signaling:
        addr: 12345
        proto: http
```

## <a name="setting-up-local-media"></a><span data-ttu-id="79936-118">ローカルメディアのセットアップ</span><span class="sxs-lookup"><span data-stu-id="79936-118">Setting up local media</span></span>

> [!NOTE]
> <span data-ttu-id="79936-119">このセクションは、アプリケーションでホストされているメディア bot にのみ必要であり、メディアを自分でホストしていない場合はスキップできます。</span><span class="sxs-lookup"><span data-stu-id="79936-119">This section is only required for application-hosted media bots and can be skipped if you don't host media yourself.</span></span>

<span data-ttu-id="79936-120">アプリケーションホスト型メディアは、証明書と TCP トンネルを使用します。</span><span class="sxs-lookup"><span data-stu-id="79936-120">Application-hosted media uses certificates and TCP tunnels.</span></span> <span data-ttu-id="79936-121">次の手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="79936-121">The following steps are required:</span></span>

- <span data-ttu-id="79936-122">Ngrok のパブリック TCP エンドポイントには、固定の Url があります。</span><span class="sxs-lookup"><span data-stu-id="79936-122">Ngrok's public TCP endpoints have fixed URLs.</span></span> <span data-ttu-id="79936-123">これは`0.tcp.ngrok.io` `1.tcp.ngrok.io`、などです。</span><span class="sxs-lookup"><span data-stu-id="79936-123">They are `0.tcp.ngrok.io`, `1.tcp.ngrok.io`, and so on.</span></span> <span data-ttu-id="79936-124">これらの Url を参照する DNS CNAME エントリをサービスに対して設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="79936-124">You should have a DNS CNAME entry for your service that points to these URLs.</span></span> <span data-ttu-id="79936-125">この例では、という`0.bot.contoso.com`ように`0.tcp.ngrok.io`参照`1.bot.contoso.com` `1.tcp.ngrok.io`します。</span><span class="sxs-lookup"><span data-stu-id="79936-125">In this example, let's say `0.bot.contoso.com` refers to `0.tcp.ngrok.io`, `1.bot.contoso.com` refers to `1.tcp.ngrok.io`, and so on.</span></span>
- <span data-ttu-id="79936-126">Url には SSL 証明書が必要です。</span><span class="sxs-lookup"><span data-stu-id="79936-126">A SSL certificate is required for your URLs.</span></span> <span data-ttu-id="79936-127">簡単にするために、ワイルドカードドメインに対して発行された SSL 証明書を使用してください。</span><span class="sxs-lookup"><span data-stu-id="79936-127">To make it easy, use a SSL certificate issued to a wild card domain.</span></span> <span data-ttu-id="79936-128">この場合は、となり`*.bot.contoso.com`ます。</span><span class="sxs-lookup"><span data-stu-id="79936-128">In this case, it would be `*.bot.contoso.com`.</span></span> <span data-ttu-id="79936-129">この SSL 証明書は、メディア SDK によって検証されるので、bot のパブリック URL と一致している必要があります。</span><span class="sxs-lookup"><span data-stu-id="79936-129">This SSL certificate is validated by the media SDK, so it should match your bot's public URL.</span></span> <span data-ttu-id="79936-130">拇印をメモして、コンピューター証明書にインストールします。</span><span class="sxs-lookup"><span data-stu-id="79936-130">Note the thumbprint and install it in your machine certificates.</span></span>
- <span data-ttu-id="79936-131">ここで、トラフィックを localhost に転送する TCP トンネルをセットアップします。</span><span class="sxs-lookup"><span data-stu-id="79936-131">Now, setup a TCP tunnel to forward the traffic to localhost.</span></span> <span data-ttu-id="79936-132">次の行を ngrok yml に記入します。</span><span class="sxs-lookup"><span data-stu-id="79936-132">Write the following lines into your ngrok.yml:</span></span>

    ```yaml
    media:
        addr: 8445
        proto: tcp
    ```

## <a name="start-ngrok"></a><span data-ttu-id="79936-133">Ngrok の開始</span><span class="sxs-lookup"><span data-stu-id="79936-133">Start ngrok</span></span>

<span data-ttu-id="79936-134">Ngrok の構成の準備ができたので、次のように起動します。</span><span class="sxs-lookup"><span data-stu-id="79936-134">Now that the ngrok configuration is ready, launch it:</span></span>

  `ngrok.exe start -all -config <Path to your ngrok.yml>`

<span data-ttu-id="79936-135">これにより、ngrok が開始され、localhost にトンネルを提供するパブリック Url が定義されます。</span><span class="sxs-lookup"><span data-stu-id="79936-135">This starts ngrok and defines the public URLs which provide the tunnels to your localhost.</span></span> <span data-ttu-id="79936-136">出力は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="79936-136">The output looks like the following:</span></span>

```cmd
Forwarding  http://signal.ngrok.io -> localhost:12345
Forwarding  https://signal.ngrok.io -> localhost:12345
Forwarding  tcp://1.tcp.ngrok.io:12332 -> localhost:8445
```

<span data-ttu-id="79936-137">は、 `12345`信号ポート、 `8445`はアプリケーションによってホストされるポートで`12332` 、ngrok によって公開されるリモートメディアポートです。</span><span class="sxs-lookup"><span data-stu-id="79936-137">Here, `12345` is the signaling port, `8445` is the application-hosted port, and `12332` is the remote media port exposed by ngrok.</span></span> <span data-ttu-id="79936-138">への`1.bot.contoso.com`転送があることに`1.tcp.ngrok.io`注意してください。</span><span class="sxs-lookup"><span data-stu-id="79936-138">Note that we have a forwarding from `1.bot.contoso.com` to `1.tcp.ngrok.io`.</span></span> <span data-ttu-id="79936-139">これは、ボットのメディア URL として使用されます。</span><span class="sxs-lookup"><span data-stu-id="79936-139">This will be used as the media URL for the bot.</span></span> <span data-ttu-id="79936-140">当然ですが、これらのポート番号は例であり、利用可能な任意のポートを使用できます。</span><span class="sxs-lookup"><span data-stu-id="79936-140">Of course, these port numbers are just examples and you can use any available port.</span></span>

### <a name="update-code"></a><span data-ttu-id="79936-141">コードを更新する</span><span class="sxs-lookup"><span data-stu-id="79936-141">Update code</span></span>

<span data-ttu-id="79936-142">Ngrok が実行されたら、設定した構成を使用するようにコードを更新します。</span><span class="sxs-lookup"><span data-stu-id="79936-142">Once ngrok is up and running, update the code to use the config you just set up.</span></span>

#### <a name="update-signaling"></a><span data-ttu-id="79936-143">信号の更新</span><span class="sxs-lookup"><span data-stu-id="79936-143">Update signaling</span></span>

- <span data-ttu-id="79936-144">BotBuilder 呼び出しで、を ngrok で`NotificationUrl`提供された信号 URL に変更します。</span><span class="sxs-lookup"><span data-stu-id="79936-144">In the BotBuilder call, change the `NotificationUrl` to the signaling URL provided by ngrok.</span></span>

```csharp
statefulClientBuilder.SetNotificationUrl(
    new Uri("https://signal.ngrok.io/notificationEndpoint"))
```

> [!NOTE]
> <span data-ttu-id="79936-145">Ngrok によって提供されたものと`NotificationEndpoint` 、通知を受け取るコントローラパスを使用して、シグナルを置き換えます。</span><span class="sxs-lookup"><span data-stu-id="79936-145">Replace signal with the one provided by ngrok and the `NotificationEndpoint` with the controller path that receives notification.</span></span>

> <span data-ttu-id="79936-146">**重要**: in `SetNotificationUrl` URL は HTTPS である必要があります。</span><span class="sxs-lookup"><span data-stu-id="79936-146">**IMPORTANT**: The URL in `SetNotificationUrl` must be HTTPS.</span></span>

> <span data-ttu-id="79936-147">**重要**: ローカルインスタンスは、シグナリングポートの HTTP トラフィックをリッスンしている必要があります。</span><span class="sxs-lookup"><span data-stu-id="79936-147">**IMPORTANT**: Your local instance must be listening to HTTP traffic on the signaling port.</span></span> <span data-ttu-id="79936-148">呼び出しとオンライン会議のプラットフォームによって行われた要求は、エンドツーエンドの暗号化が設定されていない限り、ローカルホストの HTTP トラフィックとして表示されます。</span><span class="sxs-lookup"><span data-stu-id="79936-148">The requests made by the calls and online meetings platform will reach the bot as localhost HTTP traffic unless end-to-end encryption is set up.</span></span>

#### <a name="update-media"></a><span data-ttu-id="79936-149">メディアを更新する</span><span class="sxs-lookup"><span data-stu-id="79936-149">Update media</span></span>

<span data-ttu-id="79936-150">`MediaPlatformSettings`を次のように更新します。</span><span class="sxs-lookup"><span data-stu-id="79936-150">Update your `MediaPlatformSettings` to the following.</span></span>

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
> <span data-ttu-id="79936-151">上記で提供される証明書の拇印は、サービスの FQDN と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="79936-151">The certificate thumbprint provided above should match the Service FQDN.</span></span> <span data-ttu-id="79936-152">DNS エントリが必要なのはこのためです。</span><span class="sxs-lookup"><span data-stu-id="79936-152">That is why the DNS entries are required.</span></span>

## <a name="next-steps"></a><span data-ttu-id="79936-153">次のステップ</span><span class="sxs-lookup"><span data-stu-id="79936-153">Next steps</span></span>

<span data-ttu-id="79936-154">Bot がローカルで実行できるようになり、すべてのフローが localhost から機能するようになります。</span><span class="sxs-lookup"><span data-stu-id="79936-154">Your bot can now run locally and all the flows work from your localhost.</span></span>

## <a name="caveats"></a><span data-ttu-id="79936-155">べき</span><span class="sxs-lookup"><span data-stu-id="79936-155">Caveats</span></span>

- <span data-ttu-id="79936-156">Ngrok 無料アカウントでは、エンドツーエンドの暗号化は提供され**ません**。</span><span class="sxs-lookup"><span data-stu-id="79936-156">Ngrok free accounts **don't** provide end-to-end encryption.</span></span> <span data-ttu-id="79936-157">HTTPS データは ngrok URL で終了し、データフローは ngrok からに`localhost`暗号化されていません。</span><span class="sxs-lookup"><span data-stu-id="79936-157">The HTTPS data ends at the ngrok URL and the data flows unencrypted from ngrok to `localhost`.</span></span> <span data-ttu-id="79936-158">エンドツーエンドの暗号化が必要な場合は、有料の ngrok アカウントを検討してください。</span><span class="sxs-lookup"><span data-stu-id="79936-158">If you require end-to-end encryption, consider a paid ngrok account.</span></span> <span data-ttu-id="79936-159">セキュリティで保護されたエンドツーエンドトンネルを設定する手順については、「 [TLS トンネル](https://ngrok.com/docs#tls)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="79936-159">See [TLS tunnels](https://ngrok.com/docs#tls) for steps on setting up secure end-to-end tunnels.</span></span>
- <span data-ttu-id="79936-160">Bot のコールバック URL は動的なので、着信呼び出しのシナリオでは、ngrok エンドポイントを頻繁に更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="79936-160">Because the bot callback URL is dynamic, incoming call scenarios require you to frequently update your ngrok endpoints.</span></span> <span data-ttu-id="79936-161">これを解決する1つの方法は、お客様が bot とプラットフォームをポイントできる固定サブドメインを提供する有料の ngrok アカウントを使用することです。</span><span class="sxs-lookup"><span data-stu-id="79936-161">One way to fix this is to use a paid ngrok account which provides fixed subdomains to which you can point your bot and the platform.</span></span>
- <span data-ttu-id="79936-162">Ngrok トンネルは、 [Azure Service Fabric](/azure/service-fabric/service-fabric-overview)でも使用できます。</span><span class="sxs-lookup"><span data-stu-id="79936-162">Ngrok tunnels can also be used with [Azure Service Fabric](/azure/service-fabric/service-fabric-overview).</span></span> <span data-ttu-id="79936-163">これを行う方法の例については、「Boe-bot」の[サンプルアプリ](/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/LocalMediaSamples/HueBot/HueBot)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="79936-163">For an example of how to do this, see the [HueBot sample app](/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/LocalMediaSamples/HueBot/HueBot).</span></span>
