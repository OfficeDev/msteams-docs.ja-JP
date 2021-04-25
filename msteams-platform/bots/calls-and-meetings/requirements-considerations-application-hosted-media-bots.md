---
title: アプリケーションホスト型メディア ボットの要件と考慮事項
description: Microsoft Teams 用のアプリケーションホスト型メディア ボットの作成に関連する重要な要件と考慮事項について説明します。
ms.topic: conceptual
keywords: アプリケーションホスト型メディア Windows サーバー azure vm
ms.date: 11/16/2018
ms.openlocfilehash: 4a191bbde6b592c74930069d794ff37273785c1b
ms.sourcegitcommit: dd2220f691029d043aaddfc7c229e332735acb1d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2021
ms.locfileid: "51995954"
---
# <a name="requirements-and-considerations-for-application-hosted-media-bots"></a>アプリケーションホスト型メディア ボットの要件と考慮事項

アプリケーションホスト型メディア ボットでは、音声およびビデオ メディア ストリーム[ `Microsoft.Graph.Communications.Calls.Media` にアクセスするために .NET](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/)ライブラリが必要です。 ボットは、Azure の Windows Server コンピューターまたは Windows Server ゲスト オペレーティング システム (OS) に展開する必要があります。

> [!NOTE]
> * メッセージングおよび対話型音声応答 (IVR) ボットを開発するためのガイダンスは、アプリケーションホスト型メディア ボットの構築には完全には適用されません。
> * Microsoft Real-time Media Platform for bots は開発者向けプレビューに含まれるので、このドキュメントのガイダンスは変更される可能性があります。

## <a name="c-or-net-and-windows-server-for-development"></a>C# .NET と Windows Server の開発

アプリケーションホスト型メディア ボットには、次の情報が必要です。

- ボットは、Microsoft Azure で開発C#標準.NET Framework展開する必要があります。 C++ API または Node.js API を使用してリアルタイム メディアにアクセスすることはできません。アプリケーションホスト型メディア ボットでは .NET Core はサポートされていません。

- ボットは、次のいずれかの Azure サービス環境内でホストできます。
    - クラウド サービス。
    - 仮想マシン スケール セット (VMSS) を備える Service Fabric。
    - サービスとしてのインフラストラクチャ (IaaS) 仮想マシン (VM)。  
  
- ボットを Azure Web アプリとして展開することはできません。

- ボットは、.NET ライブラリの最新バージョンで実行されている `Microsoft.Graph.Communications.Calls.Media` 必要があります。 ボットでは [、NuGet](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/)パッケージの最新バージョンまたは 3 か月以内のバージョンを使用する必要があります。 古いバージョンのライブラリは廃止され、数か月後には機能しません。 ライブラリを `Microsoft.Graph.Communications.Calls.Media` 最新の状態に保つことで、ボットと Microsoft Teams 間の最適な相互運用性が保証されます。

次のセクションでは、リアルタイム メディア通話の場所の詳細について説明します。

## <a name="real-time-media-calls-stay-where-they-are-created"></a>リアルタイム のメディア通話は、作成された場所にとどまる

リアルタイムのメディア通話は、作成されたコンピューターに残っています。 リアルタイムのメディア通話は、呼び出しを受け入れるか開始した仮想マシン (VM) インスタンスにピン留めされます。 Microsoft Teams の呼び出しまたは会議フローからその VM インスタンスへのメディア、およびボットが Microsoft Teams に送り返すメディアも、その VM から発信される必要があります。 VM の停止時にリアルタイムのメディア呼び出しが進行中の場合、これらの呼び出しは突然終了します。 ボットが保留中の VM シャットダウンに関する事前知識を持っている場合は、呼び出しを終了できます。

次のセクションでは、アプリケーションホスト型メディア ボットのアクセシビリティの詳細について説明します。

## <a name="application-hosted-media-bots-accessible-on-the-internet"></a>インターネット上でアクセス可能なアプリケーションホスト型メディア ボット

アプリケーションホスト型メディア ボットは、インターネット上で直接アクセスできる必要があります。 これらのボットには、次の機能が含まれる必要があります。

- Azure でアプリケーションホスト型メディア ボットをホストする各 VM インスタンスは、インスタンス レベルのパブリック IP アドレス (ILPIP) を使用してインターネットから直接アクセスできる必要があります。
    - Azure Cloud Service の ILPIP を取得および構成するには、「インスタンス レベルのパブリック IP クラシックの概要 [」を参照してください](/azure/virtual-network/virtual-networks-instance-level-public-ip)。
    - VM スケール セットの ILPIP を構成するには、「仮想マシンごとの [パブリック IPv4」を参照してください](/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-networking#public-ipv4-per-virtual-machine)。
- アプリケーションホスト型メディア ボットをホストするサービスでは、特定のインスタンスにマップされるパブリック向けポートを使用して各 VM インスタンスを構成する必要があります。
    - Azure Cloud Service の場合、これにはインスタンス入力エンドポイントが必要です。 詳細については [、「Azure でロール インスタンスの通信を有効にする」を参照してください](/azure/cloud-services/cloud-services-enable-communication-role-instances)。
    - VM スケール セットの場合、ロード バランサーの NAT ルールを構成する必要があります。 詳細については [、「Azure の仮想ネットワークと仮想マシン」を参照してください](/azure/virtual-machines/windows/network-overview)。
- アプリケーションホスト型メディア ボットは、ボット フレームワーク エミュレーターではサポートされていません。

次のセクションでは、アプリケーションホスト型メディア ボットのスケーラビリティとパフォーマンスに関する考慮事項の詳細について説明します。

## <a name="scalability-and-performance-considerations"></a>スケーラビリティとパフォーマンスに関する検討事項

アプリケーションホスト型メディア ボットには、次のスケーラビリティとパフォーマンスに関する考慮事項が必要です。

## <a name="code-sample"></a>コード サンプル

アプリケーションホスト型メディア ボットのサンプルは次のとおりです。

| **サンプル名** | **説明** | **Graph** |
|------------|-------------|-----------|
| ローカル メディアのサンプル | さまざまなローカル メディア シナリオを示すサンプル。 | [View](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/LocalMediaSamples) |
| リモート メディアのサンプル | さまざまなリモート メディア シナリオを示すサンプル。 | [View](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/RemoteMediaSamples) |

## <a name="see-also"></a>関連項目

- [グラフ呼び出し SDK のドキュメント](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/)
- ボットでは、メッセージング ボットよりも多くのコンピューティングとネットワーク帯域幅の容量が必要であり、運用コストが大幅に高くなります。 リアルタイムのメディア ボット開発者は、ボットのスケーラビリティを慎重に測定し、ボットが管理できる以上の同時呼び出しを受け入れなかねない必要があります。 ビデオが有効なボットは、RAW RGB24 または NV12 ビデオ形式を使用する場合、CPU コアごとに 1 つまたは 2 つの同時メディア セッションのみを維持できます。
- リアルタイム メディア プラットフォームでは、現在、VM で使用できるグラフィックス処理ユニット (GPU) を利用して H.264 ビデオ エンコードまたはデコードをオフロードできません。 代わりに、ビデオエンコードとデコードは CPU 上のソフトウェアで行われます。 GPU が使用可能な場合、ボットが 3D グラフィックス エンジンを使用している場合など、ボットは独自のグラフィックス レンダリングで GPU を利用します。
- リアルタイム メディア ボットをホストする VM インスタンスには、少なくとも 2 つの CPU コアが必要です。 Azure では、Dv2 シリーズ仮想マシンをお勧めします。 他の Azure VM の種類では、4 つの仮想 CPU (vCPU) を持つシステムが必要な最小サイズです。 Azure VM の種類の詳細については、「Azure のドキュメント」 [を参照してください](/azure/virtual-machines/windows/sizes-general)。

次のセクションでは、さまざまなローカル メディア シナリオを示すサンプルを示します。

## <a name="samples-and-additional-resources"></a>サンプルと追加のリソース

- [サンプル アプリケーション](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/LocalMediaSamples)
- [SDK ドキュメントを呼び出すグラフ](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/)

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [サポートされているメディア形式](~/resources/media-formats.md)
