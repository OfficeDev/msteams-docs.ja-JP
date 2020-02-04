---
title: アプリケーションホスト型メディアのボットの要件と考慮事項
description: Microsoft Teams のアプリケーションホスト型メディアボットの作成に関連する重要な要件と考慮事項について説明します。
keywords: アプリケーションホスト型メディア windows server azure vm
ms.date: 11/16/2018
ms.openlocfilehash: f5b721edacb11e867d05c8213b74036cb51f419c
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674786"
---
# <a name="requirements-and-considerations-for-application-hosted-media-bots"></a>アプリケーションホスト型メディアのボットの要件と考慮事項

メッセージングおよび対話型音声応答 (IVR) の bot を開発するためのすべてのガイダンスは、アプリケーションでホストされるメディア bot を構築する場合にも同様に適用されます。 この記事では、アプリケーションホスト型メディアボットを開発して実行するための重要な要件と考慮事項について説明します。

> [!NOTE]
> Bot 用の Microsoft のリアルタイムメディアプラットフォームは開発者向けのプレビュー版であるため、この記事のガイダンスは変更される可能性があります。

## <a name="application-hosted-media-bot-development-requires-cnet-and-windows-server"></a>アプリケーションホスト型メディアボット開発には C#/.NET および Windows Server が必要です。

- アプリケーションホスト型メディアボットには、 `Microsoft.Graph.Communications.Calls.Media` .net ライブラリ ([ここ](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/)ではオーディオおよびビデオメディアストリームにアクセスできる) が必要であり、ボットは windows server コンピューター (または、Azure の windows server ゲスト OS) に展開されている必要があります。 そのため、ボットは C# および標準の .NET Framework で開発され、Microsoft Azure に展開されている必要があります。 C++ または node.js Api を使用してリアルタイムメディアにアクセスすることはできません。また、アプリケーションホスト型メディア bot に対して .NET Core はサポートされていません。

- アプリケーションホスト型メディアボットは、次のいずれかの Azure サービス環境でホストできます。
  - クラウドサービス。
  - 仮想マシンスケールセット (VMSS) を使用したサービスファブリック。
  - サービスとしてのインフラストラクチャ (IaaS) 仮想マシン (VM)。  
  
- アプリケーションホスト型のメディア bot は、Azure Web App として展開できません。

- アプリケーションホスト型のメディアボットは、最新バージョンの`Microsoft.Graph.Communications.Calls.Media` .net ライブラリで実行されている必要があります。 Bot は、 [NuGet パッケージ](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/)の最新バージョンを使用しているか、過去3か月を超えていないバージョンを使用する必要があります。 以前のバージョンのライブラリは廃止され、数か月後に機能しなくなる可能性があります。 `Microsoft.Graph.Communications.Calls.Media`ライブラリを最新の状態に保つことにより、Bot と Microsoft Teams の間の相互運用性が向上します。

## <a name="real-time-media-calls-stay-on-the-machine-where-they-were-created"></a>リアルタイムメディア通話は、作成されたコンピューター上に保持されます。

- リアルタイムメディア呼び出しは、通話を承諾または開始した仮想マシン (VM) のインスタンスに固定されます。 Microsoft Teams の通話または会議のメディアは、その VM インスタンスに送信されます。また、ボットが Microsoft Teams に返送するメディアも、その VM から発信される必要があります。
- VM の停止時に実行中のリアルタイムメディア通話がある場合は、それらの通話は突然終了されます。 Bot が保留中の VM シャットダウンに関する事前知識を持っている場合は、呼び出しを "正常に" 終了することができます。

## <a name="application-hosted-media-bots-must-be-directly-accessible-on-the-internet"></a>アプリケーションによってホストされているメディアボットはインターネット上で直接アクセスできる必要がある

- Azure でアプリケーションホスト型メディア bot をホストする各 VM インスタンスは、インスタンスレベルのパブリック IP アドレス (ILPIP) を使用してインターネットから直接アクセスできる必要があります。
  - Azure クラウドサービスの ILPIP を取得して構成する方法については、「[インスタンスレベルのパブリック IP (クラシック) の概要](/azure/virtual-network/virtual-networks-instance-level-public-ip)」を参照してください。
  - VM スケールセットに対して ILPIP を構成する場合は、「[仮想マシンごとにパブリック IPv4](/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-networking#public-ipv4-per-virtual-machine)」を参照してください。
- アプリケーションホスト型メディア bot をホストするサービスでは、特定のインスタンスに対応する公開ポートを使用して各 VM インスタンスを構成する必要もあります。
  - Azure クラウドサービスの場合は、インスタンス入力エンドポイントが必要です。「 [Azure のロールインスタンスの通信を有効にする](/azure/cloud-services/cloud-services-enable-communication-role-instances)」を参照してください。
  - VM スケールセットの場合は、ロードバランサーの NAT ルールを構成する必要があります。「 [Azure の仮想ネットワークと仮想マシン](/azure/virtual-machines/windows/network-overview)」を参照してください。
- アプリケーションでホストされているメディアボットは、Bot フレームワークエミュレーターではサポートされていません。

## <a name="scalability-and-performance-considerations"></a>スケーラビリティとパフォーマンスに関する検討事項

- アプリケーションホスト型メディアボットには、メッセージング bot よりも多くのコンピューティングおよびネットワーク (帯域幅) 容量が必要であり、運用コストが大幅に高くなる可能性があります。 リアルタイムメディアボット開発者は、bot の拡張性を慎重に測定して、bot が管理できるよりも多くの同時通話を受け入れないようにしてください。 ビデオ対応ボットは、CPU コアごとに1つまたは2つの同時メディアセッションを維持できます (「raw」 RGB24 または NV12 ビデオ形式を使用している場合)。
- 現在、リアルタイムメディアプラットフォームは、VM 上で使用可能なすべてのグラフィックス処理装置 (GPU) を、オフロードにすることができません。264ビデオエンコード/デコード。 代わりに、ビデオエンコードとデコードは CPU のソフトウェアで行われます。 GPU が使用可能な場合、bot は独自のグラフィックスレンダリングに対してこの機能を利用できます (bot が3D グラフィックスエンジンを使用している場合など)。
- リアルタイムメディアボットをホストする VM インスタンスには、少なくとも2つの CPU コアが必要です。 Azure の場合は、Dv2 シリーズの仮想マシンをお勧めします。 その他の Azure VM の場合は、4つの仮想 Cpu (vCPU) を備えたシステムに必要な最小サイズを指定します。 Azure VM の種類の詳細については、 [azure のドキュメント](/azure/virtual-machines/windows/sizes-general)を参照してください。

## <a name="samples-and-additional-resources"></a>サンプルとその他の技術情報

- [サンプルアプリケーション](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/LocalMediaSamples)
- [グラフ呼び出し SDK ドキュメント](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/)
