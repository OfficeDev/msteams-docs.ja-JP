---
title: アプリケーションホスト型メディア ボットの要件と考慮事項
description: Microsoft Teams のアプリケーション ホスト型メディア ボットの作成に関連する重要な要件と考慮事項について説明します。
ms.topic: conceptual
keywords: アプリケーションホスト型メディア Windows サーバー Azure vm
ms.date: 11/16/2018
ms.openlocfilehash: bf75b7f689713f16cb3ff9ff4313ab829b5cc2d6
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014489"
---
# <a name="requirements-and-considerations-for-application-hosted-media-bots"></a>アプリケーションホスト型メディア ボットの要件と考慮事項

メッセージングおよび対話型音声応答 (IVR) ボットを開発するためのガイダンスのすべてが、アプリケーションホスト型メディア ボットの構築にも同じように適用されるわけではありません。 この記事では、アプリケーションホスト型メディア ボットの開発と実行に関する重要な要件と考慮事項について説明します。

> [!NOTE]
> Microsoft Real-time Media Platform for Bots は開発者プレビューに含まれるため、この記事のガイダンスは変更される可能性があります。

## <a name="application-hosted-media-bot-development-requires-cnet-and-windows-server"></a>アプリケーションホスト型メディア ボット開発には C#/.NET と Windows Server が必要

- アプリケーションでホストされるメディア ボットには.NET ライブラリ (オーディオとビデオのメディア ストリームにアクセスするためにここで利用できます)、ボットは Windows Server コンピューター (または Azure の Windows Server ゲスト OS) に展開する必要があります。 `Microsoft.Graph.Communications.Calls.Media` [](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/) したがって、ボットは C# と標準の .NET Framework で開発し、Microsoft Azure に展開する必要があります。 C++ または Node.js API を使用してリアルタイム メディアにアクセスすることはできません。また、アプリケーションホスト型メディア ボットでは .NET Core はサポートされていません。

- アプリケーションホスト型メディア ボットは、次のいずれかの Azure サービス環境内でホストできます。
  - クラウド サービス。
  - 仮想マシン スケール セット (VMSS) を含む Service Fabric。
  - サービスとしてのインフラストラクチャ (IaaS) 仮想マシン (VM)。  
  
- アプリケーションホスト型メディア ボットは、Azure Web App として展開できない。

- アプリケーションホスト型メディア ボットは、最新バージョンの .NET ライブラリで実行されている `Microsoft.Graph.Communications.Calls.Media` 必要があります。 ボットは [、NuGet](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/)パッケージの最新の利用可能なバージョン、または 3 か月以上前のバージョンを使用する必要があります。 古いバージョンのライブラリは廃止され、数か月後には機能しない可能性があります。 ライブラリを `Microsoft.Graph.Communications.Calls.Media` 最新の状態に保つことで、ボットと Microsoft Teams の間の最適な相互運用性が確保されます。

## <a name="real-time-media-calls-stay-on-the-machine-where-they-were-created"></a>リアルタイム メディア通話は、作成されたコンピューター上に残る

- リアルタイムメディア通話は、通話を受け付けまたは開始した仮想マシン (VM) インスタンスにピン留めされます。 Microsoft Teams の通話または会議からのメディアは、その VM インスタンスに流れ、ボットが Microsoft Teams に送り返すメディアもその VM から発信される必要があります。
- VM の停止時に進行中のリアルタイム メディア呼び出しがある場合、それらの呼び出しは突然終了されます。 保留中の VM シャットダウンに関する事前の知識があるボットは、呼び出しを "正常に" 終了しようとすることができます。

## <a name="application-hosted-media-bots-must-be-directly-accessible-on-the-internet"></a>アプリケーションホスト型メディア ボットは、インターネット上で直接アクセスできる必要があります。

- Azure でアプリケーションホスト型メディア ボットをホストする各 VM インスタンスは、インスタンス レベルのパブリック IP アドレス (ILPIP) を使用してインターネットから直接アクセスできる必要があります。
  - Azure クラウド サービスの ILPIP を取得および構成するには、「インスタンス レベルのパブリック [IP (クラシック) の概要」を参照してください](/azure/virtual-network/virtual-networks-instance-level-public-ip)。
  - VM スケール セットの ILPIP を構成するには、仮想マシンごとの [パブリック IPv4 を参照してください](/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-networking#public-ipv4-per-virtual-machine)。
- また、アプリケーションホスト型メディア ボットをホストするサービスは、特定のインスタンスにマップされる公開ポートを使用して各 VM インスタンスを構成する必要があります。
  - Azure クラウド サービスの場合、これにはインスタンス入力エンドポイントが必要です。「Azure [でロール インスタンスの通信を有効にする」を参照してください](/azure/cloud-services/cloud-services-enable-communication-role-instances)。
  - VM スケール セットの場合、ロード バランサーの NAT ルールを構成する必要があります。 [Azure の仮想ネットワークと仮想マシンを参照してください](/azure/virtual-machines/windows/network-overview)。
- アプリケーションホスト型メディア ボットは、Bot Framework エミュレーターではサポートされていません。

## <a name="scalability-and-performance-considerations"></a>スケーラビリティとパフォーマンスに関する検討事項

- アプリケーションホスト型メディア ボットは、メッセージング ボットよりも多くのコンピューティングおよびネットワーク (帯域幅) 容量を必要とし、運用コストが大幅に高くなる可能性があります。 リアルタイム メディア ボットの開発者は、ボットのスケーラビリティを慎重に測定し、ボットが管理できる数を超える同時呼び出しを受け付けずにいなければならない。 ビデオ対応ボットは、CPU コアごとに 1 つまたは 2 つの同時メディア セッションのみを維持できる場合があります ("raw" RGB24 または NV12 ビデオ形式を使用する場合)。
- 現在、リアルタイム メディア プラットフォームでは、VM で利用可能なグラフィックス処理ユニット (GPU) を利用して H.264 ビデオ エンコード/デコードをオフロードしている必要があります。 代わりに、ビデオエンコードとデコードは CPU 上のソフトウェアで行われます。 GPU が利用可能な場合、ボットは独自のグラフィックス レンダリングで GPU を利用できます (ボットが 3D グラフィックス エンジンを使用している場合など)。
- リアルタイム メディア ボットをホストする VM インスタンスには、少なくとも 2 つの CPU コアが必要です。 Azure では、Dv2 シリーズ仮想マシンをお勧めします。 その他の Azure VM の種類では、4 つの仮想 CPU (vCPU) を備えるシステムが必要な最小サイズです。 Azure VM の種類の詳細については、Azure のドキュメントを [参照してください](/azure/virtual-machines/windows/sizes-general)。

## <a name="samples-and-additional-resources"></a>サンプルとその他のリソース

- [サンプル アプリケーション](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/LocalMediaSamples)
- [Graph Calling SDK ドキュメント](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/)
