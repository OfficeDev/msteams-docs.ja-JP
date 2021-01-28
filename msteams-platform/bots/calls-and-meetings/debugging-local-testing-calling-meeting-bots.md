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
# <a name="how-to-develop-calling-and-online-meeting-bots-on-your-local-pc"></a>ローカル PC で通話ボットとオンライン会議ボットを開発する方法

アプリ[の実行とデバッグでは](../../concepts/build-and-test/debug.md)[、ngrok](https://ngrok.com)を使用してローカル コンピューターとインターネットの間にトンネルを作成する方法について説明します。 このトピックでは、ngrok とローカル PC を使用して、通話やオンライン会議をサポートするボットを開発する方法について説明します。

メッセージング ボットは HTTP を使用しますが、通話ボットとオンライン会議ボットは下位レベルの TCP を使用します。 Ngrok は、HTTP トンネルに加えて TCP トンネルもサポートしています。その方法については、以下を参照してください。

## <a name="configuring-ngrokyml"></a>ngrok.yml の構成

[ngrok に移動し](https://ngrok.com)、無料アカウントにサインアップするか、既存のアカウントにログインします。 ログインしたら、ダッシュボードに [移動して](https://dashboard.ngrok.com) 、authtoken を取得します。

ngrok 構成ファイルを作成し (このファイルの場所の詳細については、このファイルを参照 `ngrok.yml` してください)、次の行を追加します。 [](https://ngrok.com/docs#config)

  `authtoken: <Your-AuthToken>`

## <a name="setting-up-signaling"></a>シグナリングの設定

通話 [とオンライン会議](./calls-meetings-bots-overview.md)のボットでは、通話信号について説明しました。ボットが通話中に新しい通話やイベントを検出して応答する方法について説明しました。 呼び出し信号イベントは、HTTP POST を介してボットの呼び出しエンドポイントに送信されます。

ボットのメッセージング API と同様に、リアルタイム メディア プラットフォームがボットと通信するには、ボットがインターネット上で到達可能である必要があります。 Ngrok を使用すると、この操作が簡単になります。ngrok.yml に次の行を追加します。

```yaml
tunnels:
    signaling:
        addr: 12345
        proto: http
```

## <a name="setting-up-local-media"></a>ローカル メディアの設定

> [!NOTE]
> このセクションは、アプリケーションホスト型メディア ボットでのみ必要であり、メディアを自分でホストしない場合はスキップできます。

アプリケーションホスト型メディアは、証明書と TCP トンネルを使用します。 次の手順が必要です。

- Ngrok のパブリック TCP エンドポイントの URL は固定されています。 これらは `0.tcp.ngrok.io` 、 `1.tcp.ngrok.io` 次の場合などです。 これらの URL をポイントするサービスの DNS CNAME エントリが必要です。 この例では、参照、参照、など `0.bot.contoso.com` `0.tcp.ngrok.io` `1.bot.contoso.com` `1.tcp.ngrok.io` とします。
- URL には SSL 証明書が必要です。 簡単に実行するには、ワイルドカード ドメインに発行された SSL 証明書を使用します。 この場合は、 `*.bot.contoso.com` . この SSL 証明書はメディア SDK によって検証されます。そのため、ボットのパブリック URL と一致する必要があります。 拇印をメモし、コンピューターの証明書にインストールします。
- 次に、トラフィックを localhost に転送する TCP トンネルをセットアップします。 ngrok.yml に次の行を記述します。

    ```yaml
    media:
        addr: 8445
        proto: tcp
    ```

## <a name="start-ngrok"></a>ngrok を起動する

ngrok 構成の準備が整ったので、次の方法で起動します。

  `ngrok.exe start -all -config <Path to your ngrok.yml>`

これにより ngrok が開始され、localhost へのトンネルを提供するパブリック URL が定義されます。 出力は次のようになります。

```cmd
Forwarding  http://signal.ngrok.io -> localhost:12345
Forwarding  https://signal.ngrok.io -> localhost:12345
Forwarding  tcp://1.tcp.ngrok.io:12332 -> localhost:8445
```

次に示すのは、信号ポートであり、アプリケーションでホストされるポートであり、ngrok によって公開されるリモート メディア `12345` `8445` `12332` ポートです。 転送先が設定されている点に注意 `1.bot.contoso.com` してください `1.tcp.ngrok.io` 。 これは、ボットのメディア URL として使用されます。 もちろん、これらのポート番号は単なる例であり、使用可能な任意のポートを使用できます。

### <a name="update-code"></a>コードを更新する

ngrok が稼働したら、設定した構成を使用するコードを更新します。

#### <a name="update-signaling"></a>更新信号

- BotBuilder 呼び出しで `NotificationUrl` 、ngrok によって提供される信号 URL に変更します。

```csharp
statefulClientBuilder.SetNotificationUrl(
    new Uri("https://signal.ngrok.io/notificationEndpoint"))
```

> [!NOTE]
> 信号を ngrok によって提供される信号に置き換え、通知を受け取るコントローラー パス `NotificationEndpoint` に置き換える。

> **重要**: URL は HTTPS `SetNotificationUrl` である必要があります。

> **重要**: ローカル インスタンスは信号ポートで HTTP トラフィックをリッスンしている必要があります。 通話およびオンライン会議プラットフォームによって行われた要求は、エンド to エンドの暗号化が設定されていない限り、localhost HTTP トラフィックとしてボットに到達します。

#### <a name="update-media"></a>メディアを更新する

次の `MediaPlatformSettings` 手順に従って更新します。

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
> 上記の証明書の拇印は、サービスの FQDN と一致している必要があります。 DNS エントリが必要になるのは、この理由です。

## <a name="next-steps"></a>次の手順

ボットをローカルで実行し、すべてのフローが localhost から機能する。

## <a name="caveats"></a>注意点

- Ngrok 無料アカウント **では、エンドツーエンド** の暗号化は提供しません。 HTTPS データは ngrok URL で終わり、データフローは ngrok から暗号化されません `localhost` 。 エンドツーエンドの暗号化が必要な場合は、有料の ngrok アカウントを検討してください。 セキュリティ [で保護されたエンド](https://ngrok.com/docs#tls) エンド トンネルを設定する手順については、「TLS トンネル」を参照してください。
- ボットコールバック URL は動的なので、着信呼び出しのシナリオでは、ngrok エンドポイントを頻繁に更新する必要があります。 これを修正する 1 つの方法は、ボットとプラットフォームを指し示す固定サブドメインを提供する有料の ngrok アカウントを使用する方法です。
- Ngrok トンネルは Azure Service Fabric でも [使用できます](/azure/service-fabric/service-fabric-overview)。 これを行う方法の例については、HueBot サンプル アプリ [をご覧ください](/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/LocalMediaSamples/HueBot/HueBot)。
