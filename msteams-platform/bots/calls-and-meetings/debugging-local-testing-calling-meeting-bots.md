---
title: ローカルで呼び出しや会議用ボットのデバッグを行う
description: ngrok を使用して、ローカル PC で通話とオンライン会議ボットを開発する方法について学習します。
ms.topic: how-to
keywords: ローカル開発 ngrok トンネル
ms.date: 11/18/2018
ms.openlocfilehash: d61c380fda941618a769ad3fffa053b2a4800de9
ms.sourcegitcommit: 5b3ba227c2e5e6f7a2c629961993f168da6a504d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2021
ms.locfileid: "51634728"
---
# <a name="develop-calling-and-online-meeting-bots-on-your-local-pc"></a>ローカル PC で通話およびオンライン会議ボットを開発する

[ [アプリの実行とデバッグ](../../concepts/build-and-test/debug.md) ] では [、ngrok](https://ngrok.com) を使用してローカル コンピューターとインターネットの間にトンネルを作成する方法について説明します。 このトピックでは、ngrok とローカル PC を使用して、通話やオンライン会議をサポートするボットを開発する方法について説明します。

メッセージング ボットは HTTP を使用しますが、通話とオンライン会議ボットは下位レベルの TCP を使用します。 Ngrok は、HTTP トンネルに加えて TCP トンネルもサポートします。 

## <a name="configure-ngrokyml"></a>ngrok.yml を構成する

[ngrok に移動し](https://ngrok.com)、無料アカウントにサインアップするか、既存のアカウントにログインします。 サインインした後、ダッシュボードに [移動し](https://dashboard.ngrok.com) 、authtoken を取得します。

ngrok 構成ファイルを作成し `ngrok.yml` 、次の行を追加します。 ファイルの場所の詳細については [、「ngrok」を参照してください](https://ngrok.com/docs#config)。

  `authtoken: <Your-AuthToken>`

## <a name="set-up-signaling"></a>シグナリングのセットアップ

[ [通話とオンライン会議の](./calls-meetings-bots-overview.md)ボット] では、ボットが通話中に新しい通話やイベントを検出して応答する方法について、通話シグナリングについて説明しました。 呼び出しシグナル イベントは、HTTP POST を介してボットの呼び出しエンドポイントに送信されます。

ボットのメッセージング API と同様に、リアルタイム メディア プラットフォームがボットと通信するには、ボットがインターネット上で到達可能である必要があります。 Ngrok は、この単純な操作を行います。 ngrok.yml に次の行を追加します。

```yaml
tunnels:
    signaling:
        addr: 12345
        proto: http
```

## <a name="set-up-local-media"></a>ローカル メディアのセットアップ

> [!NOTE]
> このセクションは、アプリケーションホスト型メディア ボットでのみ必要であり、自分でメディアをホストしない場合はスキップできます。

アプリケーションホスト型メディアは、証明書と TCP トンネルを使用します。 以下の手順が必要です。

1. Ngrok のパブリック TCP エンドポイントには固定 URL があります。 これらは `0.tcp.ngrok.io` `1.tcp.ngrok.io` 、、、などです。 これらの URL をポイントするサービスの DNS CNAME エントリが必要です。 たとえば、参照、参照、などと `0.bot.contoso.com` `0.tcp.ngrok.io` `1.bot.contoso.com` `1.tcp.ngrok.io` します。
2. URL には SSL 証明書が必要です。 簡単に行う場合は、ワイルドカード ドメインに発行された SSL 証明書を使用します。 この場合は、 `*.bot.contoso.com` です。 この SSL 証明書はメディア SDK によって検証されます。そのため、ボットのパブリック URL と一致する必要があります。 拇印をメモし、コンピューター証明書にインストールします。
3. 次に、トラフィックを localhost に転送する TCP トンネルをセットアップします。 ngrok.yml に次の行を記述します。

    ```yaml
    media:
        addr: 8445
        proto: tcp
    ```

## <a name="start-ngrok"></a>ngrok を開始する

ngrok 構成の準備が整ったので、次の方法で起動します。

  `ngrok.exe start -all -config <Path to your ngrok.yml>`

これは ngrok を開始し、ローカル ホストへのトンネルを提供するパブリック URL を定義します。 出力の例を次に示します。

```cmd
Forwarding  http://signal.ngrok.io -> localhost:12345
Forwarding  https://signal.ngrok.io -> localhost:12345
Forwarding  tcp://1.tcp.ngrok.io:12332 -> localhost:8445
```

ここでは、シグナリング ポート、アプリケーションホストポート、および ngrok によって公開される `12345` リモート メディア `8445` `12332` ポートを示します。 からへの転送があります `1.bot.contoso.com` `1.tcp.ngrok.io` 。 これは、ボットのメディア URL として使用されます。 もちろん、これらのポート番号は単なる例であり、使用可能な任意のポートを使用できます。

### <a name="update-code"></a>コードを更新する

ngrok が稼働した後、セットアップした構成を使用するコードを更新します。

#### <a name="update-signaling"></a>信号の更新

BotBuilder 呼び出しで `NotificationUrl` 、ngrok によって提供されるシグナリング URL に変更します。

```csharp
statefulClientBuilder.SetNotificationUrl(
    new Uri("https://signal.ngrok.io/notificationEndpoint"))
```

> [!NOTE]
> 信号を ngrok が提供するパスに置き換え、通知を受け取る `NotificationEndpoint` コントローラー パスに置き換える。

> [!IMPORTANT]
> * URL は HTTPS `SetNotificationUrl` である必要があります。
> 
> ローカル インスタンスは、シグナリング ポートで HTTP トラフィックをリッスンしている必要があります。 通話とオンライン会議プラットフォームによって行われた要求は、エンドツーエンドの暗号化が設定されていない限り、ボットに localhost HTTP トラフィックとして到達します。

#### <a name="update-media"></a>メディアの更新

次のように `MediaPlatformSettings` 更新します。

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
> で提供される証明書の拇印は `MediaPlatformSettings` 、サービス FQDN と一致する必要があります。 DNS エントリが必要な理由です。

## <a name="caveats"></a>注意点

- Ngrok 無料アカウント **は、エンドツーエンド** の暗号化を提供しません。 HTTPS データは ngrok URL で終了し、データ フローは ngrok から . `localhost` エンドツーエンドの暗号化が必要な場合は、有料の ngrok アカウントを検討してください。 セキュリティ [で保護されたエンドツーエンド トンネル](https://ngrok.com/docs#tls) をセットアップする手順については、「TLS トンネル」を参照してください。
- ボットコールバック URL は動的なので、着信呼び出しのシナリオでは、ngrok エンドポイントを頻繁に更新する必要があります。 これを修正する 1 つの方法は、ボットとプラットフォームをポイントできる固定サブドメインを提供する有料の ngrok アカウントを使用する方法です。
- Ngrok トンネルは Azure Service [Fabric でも使用できます](/azure/service-fabric/service-fabric-overview)。 これを行う方法の例については、「HueBot サンプル アプリ [」を参照してください](/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/LocalMediaSamples/HueBot/HueBot)。
