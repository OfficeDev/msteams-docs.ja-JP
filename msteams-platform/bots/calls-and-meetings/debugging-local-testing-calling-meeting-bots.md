---
title: ローカルで呼び出しや会議用ボットのデバッグを行う
description: ngrok を使用して、ローカル PC で通話やオンライン会議ボットを開発する方法についても学びます。
ms.topic: how-to
ms.localizationpriority: medium
keywords: ローカル開発 ngrok トンネル
ms.date: 11/18/2018
ms.openlocfilehash: 7f85243e0a5d94711cd303ff542decd3bbc7847a
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2022
ms.locfileid: "65757116"
---
# <a name="develop-calling-and-online-meeting-bots-on-your-local-pc"></a>ローカル PC で通話ボットとオンライン会議ボットを開発する

[アプリの実行とデバッグ](../../concepts/build-and-test/debug.md)で、[ngrok](https://ngrok.com) を使用してローカル コンピューターとインターネットの間にトンネルを作成する方法について説明します。 このトピックでは、ngrok とローカル PC を使用して、通話やオンライン会議をサポートするボットを開発する方法について説明します。

メッセージング ボットは HTTP を使用しますが、通話とオンライン会議ボットでは下位レベルの TCP が使用されます。 ngrok では、HTTP トンネルに加えて TCP トンネルもサポートされています。

## <a name="configure-ngrokyml"></a>ngrok.yml を構成する

[ngrok](https://ngrok.com) に移動し、無料アカウントにサインアップするか、既存のアカウントにログインします。 サインインしたら、[ダッシュボード](https://dashboard.ngrok.com)に移動し、認証トークンを取得します。

ngrok 構成ファイル `ngrok.yml` を作成し、次の行を追加します。 ファイルの場所の詳細については、[ngrok](https://ngrok.com/docs#config) を参照してください。

  `authtoken: <Your-AuthToken>`

## <a name="set-up-signaling"></a>シグナリングを設定する

[[通話とオンライン会議ボット]](./calls-meetings-bots-overview.md) では、通話中にボットが新しい通話やイベントを検出して応答する方法に関する通話シグナリングについて説明しました。 呼び出しシグナリング イベントは、HTTP POST を介してボットの呼び出しエンドポイントに送信されます。

ボットのメッセージング API と同様に、リアルタイム メディア プラットフォームがボットと通信するには、ボットにインターネット経由で到達できる必要があります。 Ngrok では、この操作が簡単になります。 ngrok.yml に次の行を追加します。

```yaml
tunnels:
    signaling:
        addr: 12345
        proto: http
```

## <a name="set-up-local-media"></a>ローカル メディアを設定する

> [!NOTE]
> このセクションは、アプリケーションでホストされるメディア ボットにのみ必要であり、自分でメディアをホストしていない場合はスキップできます。

アプリケーションでホストされるメディアでは、証明書と TCP トンネルが使用されます。 次の手順が必要です。

1. Ngrok のパブリック TCP エンドポイントには固定 URL があります。 `0.tcp.ngrok.io`これらは、次`1.tcp.ngrok.io`のように表示されます。 これらの URL を指すサービスの DNS CNAME エントリが必要です。 たとえば、`0.bot.contoso.com` が `0.tcp.ngrok.io` を参照し、`1.bot.contoso.com` が `1.tcp.ngrok.io` を参照するとします。
2. URL には SSL 証明書が必要です。 簡単にするには、ワイルドカード ドメインに発行された SSL 証明書を使用します。 この例では、`*.bot.contoso.com` になります。 この SSL 証明書はメディア SDK によって検証されるため、ボットのパブリック URL と一致する必要があります。 サムプリントをメモし、マシン証明書にインストールします。
3. 次に、トラフィックを localhost に転送する TCP トンネルを設定します。 次の行を ngrok.yml に書き込みます。

    ```yaml
    media:
        addr: 8445
        proto: tcp
    ```

## <a name="start-ngrok"></a>ngrok を開始する

ngrok 構成の準備ができたら、次のように起動します。

  `ngrok.exe start -all -config <Path to your ngrok.yml>`

これにより ngrok が開始され、localhost へのトンネルを提供するパブリック URL が定義されます。 出力の例を次に示します。

```cmd
Forwarding  http://signal.ngrok.io -> localhost:12345
Forwarding  https://signal.ngrok.io -> localhost:12345
Forwarding  tcp://1.tcp.ngrok.io:12332 -> localhost:8445
```

ここで、`12345` はシグナリング ポート、`8445` はアプリケーションでホストされるポート、`12332` は ngrok によって公開されるリモート メディア ポートです。  `1.bot.contoso.com` から `1.tcp.ngrok.io` への転送があることに注意してください。 これは、ボットのメディア URL として使用されます。 もちろん、これらのポート番号は単なる例であり、使用可能な任意のポートを使用できます。

### <a name="update-code"></a>コードを更新する

ngrok が起動して実行されたら、設定した構成を使用するようにコードを更新します。

#### <a name="update-signaling"></a>シグナリングを更新する

BotBuilder 呼び出しで、`NotificationUrl` を ngrok によって提供されるシグナリング URL に変更します。

```csharp
statefulClientBuilder.SetNotificationUrl(
    new Uri("https://signal.ngrok.io/notificationEndpoint"))
```

> [!NOTE]
> シグナルを ngrok によって提供されるものに置き換え、`NotificationEndpoint` を通知を受信するコントローラー パスに置き換えます。

> [!IMPORTANT]
>
> * `SetNotificationUrl` の URL は HTTPS である必要があります。
>
> ローカル インスタンスは、シグナリング ポートで HTTP トラフィックをリッスンしている必要があります。 通話とオンライン会議プラットフォームによって行われた要求は、エンドツーエンドの暗号化が設定されていない限り、localhost HTTP トラフィックとしてボットに到達します。

#### <a name="update-media"></a>メディアを更新する

`MediaPlatformSettings` を次のように更新します。

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
> `MediaPlatformSettings` で提供される証明書の拇印は、サービス FQDN と一致する必要があります。 そのため、DNS エントリが必要です。

## <a name="caveats"></a>警告

* ngrok の無料アカウント **はエンドツーエンドの暗号化を提供しません**。 HTTPS データは ngrok URL で終了し、データは暗号化されずに ngrok から `localhost` に流れます。 エンドツーエンドの暗号化が必要な場合は、有料の ngrok アカウントを検討してください。 安全なエンドツーエンド トンネルを設定する手順については、[TLS トンネル](https://ngrok.com/docs#tls) を参照してください。
* ボットコールバック URL は動的であるため、着信のシナリオでは、ngrok エンドポイントを頻繁に更新する必要があります。 これを修正する 1 つの方法は、ボットとプラットフォームを指すことができる固定サブドメインを提供する有料の ngrok アカウントを使用することです。
* Ngrok トンネルは、[Azure サービス ファブリック](/azure/service-fabric/service-fabric-overview) でも使用できます。 これを行う方法の例については、[[HueBot サンプル アプリ]](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/LocalMediaSamples/HueBot/HueBot) を参照してください。
