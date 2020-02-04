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
# <a name="how-to-develop-calling-and-online-meeting-bots-on-your-local-pc"></a>ローカル PC で通話およびオンライン会議のボットを開発する方法

「[アプリの実行とデバッグ](../../concepts/build-and-test/debug.md)」では、 [ngrok](https://ngrok.com)を使用して、ローカルコンピューターとインターネットとの間のトンネルを作成する方法について説明します。 このトピックでは、ngrok とローカル PC を使用して、通話とオンライン会議をサポートするボットを開発する方法について説明します。

メッセージングのボットは HTTP を使用しますが、呼び出しとオンライン会議のボットは下位レベルの TCP を使用します。 Ngrok は、HTTP トンネルに加えて TCP トンネルもサポートします。詳細については、以下を参照してください。

## <a name="configuring-ngrokyml"></a>Yml を構成する ngrok

[Ngrok](https://ngrok.com)に移動し、無料のアカウントまたはログを既存のアカウントにサインアップします。 ログインしたら、[ダッシュボード](https://dashboard.ngrok.com)に移動して authtoken を取得します。

Ngrok 構成ファイル`ngrok.yml`を作成し (このファイルが保存されている場所の詳細について[は、こちら](https://ngrok.com/docs#config)を参照してください)、次の行を追加します。

  `authtoken: <Your-AuthToken>`

## <a name="setting-up-signaling"></a>信号の設定

「[通話とオンライン会議のボット](./calls-meetings-bots-overview.md)」では、通話のシグナリングについて説明し、呼び出し中に新しい通話やイベントに対してボットが検出して応答する方法を説明しました。 通話シグナリングイベントは、ボットの呼び出しエンドポイントに HTTP POST 経由で送信されます。

Bot のメッセージング API と同様に、リアルタイムメディアプラットフォームが bot と通信するためには、ボットがインターネットを介して到達可能である必要があります。 Ngrok は、次の行を Ngrok に追加します。

```yaml
tunnels:
    signaling:
        addr: 12345
        proto: http
```

## <a name="setting-up-local-media"></a>ローカルメディアのセットアップ

> [!NOTE]
> このセクションは、アプリケーションでホストされているメディア bot にのみ必要であり、メディアを自分でホストしていない場合はスキップできます。

アプリケーションホスト型メディアは、証明書と TCP トンネルを使用します。 次の手順を実行する必要があります。

- Ngrok のパブリック TCP エンドポイントには、固定の Url があります。 これは`0.tcp.ngrok.io` `1.tcp.ngrok.io`、などです。 これらの Url を参照する DNS CNAME エントリをサービスに対して設定する必要があります。 この例では、という`0.bot.contoso.com`ように`0.tcp.ngrok.io`参照`1.bot.contoso.com` `1.tcp.ngrok.io`します。
- Url には SSL 証明書が必要です。 簡単にするために、ワイルドカードドメインに対して発行された SSL 証明書を使用してください。 この場合は、となり`*.bot.contoso.com`ます。 この SSL 証明書は、メディア SDK によって検証されるので、bot のパブリック URL と一致している必要があります。 拇印をメモして、コンピューター証明書にインストールします。
- ここで、トラフィックを localhost に転送する TCP トンネルをセットアップします。 次の行を ngrok yml に記入します。

    ```yaml
    media:
        addr: 8445
        proto: tcp
    ```

## <a name="start-ngrok"></a>Ngrok の開始

Ngrok の構成の準備ができたので、次のように起動します。

  `ngrok.exe start -all -config <Path to your ngrok.yml>`

これにより、ngrok が開始され、localhost にトンネルを提供するパブリック Url が定義されます。 出力は次のようになります。

```cmd
Forwarding  http://signal.ngrok.io -> localhost:12345
Forwarding  https://signal.ngrok.io -> localhost:12345
Forwarding  tcp://1.tcp.ngrok.io:12332 -> localhost:8445
```

は、 `12345`信号ポート、 `8445`はアプリケーションによってホストされるポートで`12332` 、ngrok によって公開されるリモートメディアポートです。 への`1.bot.contoso.com`転送があることに`1.tcp.ngrok.io`注意してください。 これは、ボットのメディア URL として使用されます。 当然ですが、これらのポート番号は例であり、利用可能な任意のポートを使用できます。

### <a name="update-code"></a>コードを更新する

Ngrok が実行されたら、設定した構成を使用するようにコードを更新します。

#### <a name="update-signaling"></a>信号の更新

- BotBuilder 呼び出しで、を ngrok で`NotificationUrl`提供された信号 URL に変更します。

```csharp
statefulClientBuilder.SetNotificationUrl(
    new Uri("https://signal.ngrok.io/notificationEndpoint"))
```

> [!NOTE]
> Ngrok によって提供されたものと`NotificationEndpoint` 、通知を受け取るコントローラパスを使用して、シグナルを置き換えます。

> **重要**: in `SetNotificationUrl` URL は HTTPS である必要があります。

> **重要**: ローカルインスタンスは、シグナリングポートの HTTP トラフィックをリッスンしている必要があります。 呼び出しとオンライン会議のプラットフォームによって行われた要求は、エンドツーエンドの暗号化が設定されていない限り、ローカルホストの HTTP トラフィックとして表示されます。

#### <a name="update-media"></a>メディアを更新する

`MediaPlatformSettings`を次のように更新します。

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
> 上記で提供される証明書の拇印は、サービスの FQDN と一致する必要があります。 DNS エントリが必要なのはこのためです。

## <a name="next-steps"></a>次のステップ

Bot がローカルで実行できるようになり、すべてのフローが localhost から機能するようになります。

## <a name="caveats"></a>べき

- Ngrok 無料アカウントでは、エンドツーエンドの暗号化は提供され**ません**。 HTTPS データは ngrok URL で終了し、データフローは ngrok からに`localhost`暗号化されていません。 エンドツーエンドの暗号化が必要な場合は、有料の ngrok アカウントを検討してください。 セキュリティで保護されたエンドツーエンドトンネルを設定する手順については、「 [TLS トンネル](https://ngrok.com/docs#tls)」を参照してください。
- Bot のコールバック URL は動的なので、着信呼び出しのシナリオでは、ngrok エンドポイントを頻繁に更新する必要があります。 これを解決する1つの方法は、お客様が bot とプラットフォームをポイントできる固定サブドメインを提供する有料の ngrok アカウントを使用することです。
- Ngrok トンネルは、 [Azure Service Fabric](/azure/service-fabric/service-fabric-overview)でも使用できます。 これを行う方法の例については、「Boe-bot」の[サンプルアプリ](/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/LocalMediaSamples/HueBot/HueBot)を参照してください。
