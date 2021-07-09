---
title: アプリケーションホスト型メディア ボットの要件と考慮事項
description: アプリケーションホスト型メディア ボットの作成に関連する重要な要件と考慮事項をMicrosoft Teams。
ms.topic: conceptual
localization_priority: Normal
keywords: アプリケーションホスト型メディア Windows サーバー azure vm
ms.date: 11/16/2018
ms.openlocfilehash: a66296951dd2f704d531840f79a4c4b955af6bdf
ms.sourcegitcommit: 3560ee1619e3ab6483a250f1d7f2ceb69353b2dc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2021
ms.locfileid: "53335362"
---
# <a name="requirements-and-considerations-for-application-hosted-media-bots"></a>アプリケーションホスト型メディア ボットの要件と考慮事項

アプリケーションホスト型メディア ボットでは、音声およびビデオ メディア ストリーム[ `Microsoft.Graph.Communications.Calls.Media` にアクセスするために .NET](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/)ライブラリが必要です。 ボットは、Azure のサーバー コンピューター Windowsサーバー ゲスト オペレーティング システム (OS) Windows展開する必要があります。

> [!NOTE]
> * メッセージングおよび対話型音声応答 (IVR) ボットを開発するためのガイダンスは、アプリケーションホスト型メディア ボットの構築には完全には適用されません。
> * Microsoft Real-time Media Platform for bots は開発者向けプレビューに含まれるので、このドキュメントのガイダンスは変更される可能性があります。

## <a name="c-or-net-and-windows-server-for-development"></a>C#または .NET および Windows サーバーの開発

アプリケーションホスト型メディア ボットには、次の情報が必要です。

- ボットは、C#および標準.NET Frameworkで開発し、Microsoft Azure。 C++ API または Node.js API を使用してリアルタイム メディアにアクセスすることはできません。アプリケーションホスト型メディア ボットでは .NET Core はサポートされていません。

- ボットは、次のいずれかの Azure サービス環境内でホストできます。
    - クラウド サービス。
    - Service Fabricスケール セット (VMSS) を使用します。
    - サービスとしてのインフラストラクチャ (IaaS) 仮想マシン (VM)。  
  
- ボットを Azure Web アプリとして展開することはできません。

- ボットは、.NET ライブラリの最新バージョンで実行されている `Microsoft.Graph.Communications.Calls.Media` 必要があります。 ボットは、最新のバージョンの NuGet パッケージ、または 3 か[月以内](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/)のバージョンを使用する必要があります。 古いバージョンのライブラリは廃止され、数か月後には機能しません。 ライブラリを `Microsoft.Graph.Communications.Calls.Media` 最新の状態に保つことで、ボットとサーバー間の最適な相互運用性がMicrosoft Teams。

次のセクションでは、リアルタイム メディア通話の場所の詳細について説明します。

## <a name="real-time-media-calls-stay-where-they-are-created"></a>リアルタイム のメディア通話は、作成された場所にとどまる

リアルタイムのメディア通話は、作成されたコンピューターに残っています。 リアルタイムのメディア通話は、呼び出しを受け入れるか開始した仮想マシン (VM) インスタンスにピン留めされます。 その VM インスタンスMicrosoft Teams呼び出しまたは会議フローからのメディア、およびボットが送信するメディアは、Microsoft Teams VM から発信する必要があります。 VM の停止時にリアルタイムのメディア呼び出しが進行中の場合、これらの呼び出しは突然終了します。 ボットが保留中の VM シャットダウンに関する事前知識を持っている場合は、呼び出しを終了できます。

次のセクションでは、アプリケーションホスト型メディア ボットのアクセシビリティの詳細について説明します。

## <a name="application-hosted-media-bots-accessible-on-the-internet"></a>インターネット上でアクセス可能なアプリケーションホスト型メディア ボット

アプリケーションホスト型メディア ボットは、インターネット上で直接アクセスできる必要があります。 これらのボットには、次の機能が含まれる必要があります。

- Azure でアプリケーションホスト型メディア ボットをホストする各 VM インスタンスは、インスタンス レベルのパブリック IP アドレス (ILPIP) を使用してインターネットから直接アクセスできる必要があります。
    - Azure Cloud Service の ILPIP を取得および構成するには、「インスタンス レベルのパブリック IP クラシックの概要 [」を参照してください](/azure/virtual-network/virtual-networks-instance-level-public-ip)。
    - VM スケール セットの ILPIP を構成するには、「仮想マシンごとの [パブリック IPv4」を参照してください](/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-networking#public-ipv4-per-virtual-machine)。
- アプリケーションホスト型メディア ボットをホストするサービスでは、特定のインスタンスにマップされるパブリック向けポートを使用して各 VM インスタンスを構成する必要があります。
    - Azure Cloud Service の場合、これにはインスタンス入力エンドポイントが必要です。 詳細については [、「Azure でロール インスタンスの通信を有効にする」を参照してください](/azure/cloud-services/cloud-services-enable-communication-role-instances)。
    - VM スケール セットの場合、ロード バランサーの NAT ルールを構成する必要があります。 詳細については [、「Azure の仮想ネットワークと仮想マシン」を参照してください](/azure/virtual-machines/windows/network-overview)。
- アプリケーションホスト型メディア ボットは、アプリケーション ホスト型メディア ボットBot Framework Emulator。

次のセクションでは、アプリケーションホスト型メディア ボットのスケーラビリティとパフォーマンスに関する考慮事項の詳細について説明します。

## <a name="scalability-and-performance-considerations"></a>スケーラビリティとパフォーマンスに関する検討事項

アプリケーションホスト型メディア ボットには、次のスケーラビリティとパフォーマンスに関する考慮事項が必要です。
- アプリケーションホスト型メディア ボットでは、メッセージング ボットよりも多くのコンピューティングおよびネットワーク (帯域幅) 容量が必要であり、運用コストが大幅に高くなる可能性があります。 リアルタイムのメディア ボット開発者は、ボットのスケーラビリティを慎重に測定し、ボットが管理できる以上の同時呼び出しを受け入れなかねない必要があります。 ビデオが有効なボットは、CPU コアごとに 1 つまたは 2 つの同時メディア セッションのみを維持できる場合があります ("raw" RGB24 または NV12 ビデオ形式を使用している場合)。
- リアルタイム メディア プラットフォームでは、現在、VM で使用可能なグラフィックス処理ユニット (GPU) を利用して H.264 ビデオ エンコード/デコードをオフロードできません。 代わりに、ビデオエンコードとデコードは CPU 上のソフトウェアで行われます。 GPU が使用可能な場合、ボットが 3D グラフィックス エンジンを使用している場合など、ボットは独自のグラフィックス レンダリングに利用できます。
- リアルタイム メディア ボットをホストする VM インスタンスには、少なくとも 2 つの CPU コアが必要です。 Azure では、Dv2 シリーズ仮想マシンをお勧めします。 他の Azure VM の種類では、4 つの仮想 CPU (vCPU) を持つシステムが必要な最小サイズです。 Azure VM の種類の詳細については、Azure のドキュメントを [参照してください](/azure/virtual-machines/windows/sizes-general)。 

## <a name="code-sample"></a>コード サンプル

アプリケーションホスト型メディア ボットのサンプルは次のとおりです。

| **サンプル名** | **説明** | **Graph** |
|------------|-------------|-----------|
| ローカル メディアのサンプル | さまざまなローカル メディア シナリオを示すサンプル。 | [View](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/LocalMediaSamples) |
| リモート メディアのサンプル | さまざまなリモート メディア シナリオを示すサンプル。 | [View](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/RemoteMediaSamples) |

## <a name="see-also"></a>関連項目

- [GraphSDK ドキュメントの呼び出し](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/)
- ボットでは、メッセージング ボットよりも多くのコンピューティングとネットワーク帯域幅の容量が必要であり、運用コストが大幅に高くなります。 リアルタイムのメディア ボット開発者は、ボットのスケーラビリティを慎重に測定し、ボットが管理できる以上の同時呼び出しを受け入れなかねない必要があります。 ビデオが有効なボットは、RAW RGB24 または NV12 ビデオ形式を使用する場合、CPU コアごとに 1 つまたは 2 つの同時メディア セッションのみを維持できます。
- リアルタイム メディア プラットフォームでは、現在、VM で使用できるグラフィックス処理ユニット (GPU) を利用して H.264 ビデオ エンコードまたはデコードをオフロードできません。 代わりに、ビデオエンコードとデコードは CPU 上のソフトウェアで行われます。 GPU が使用可能な場合、ボットが 3D グラフィックス エンジンを使用している場合など、ボットは独自のグラフィックス レンダリングで GPU を利用します。
- リアルタイム メディア ボットをホストする VM インスタンスには、少なくとも 2 つの CPU コアが必要です。 Azure では、Dv2 シリーズ仮想マシンをお勧めします。 他の Azure VM の種類では、4 つの仮想 CPU (vCPU) を持つシステムが必要な最小サイズです。 Azure VM の種類の詳細については、「Azure のドキュメント」 [を参照してください](/azure/virtual-machines/windows/sizes-general)。

次のセクションでは、さまざまなローカル メディア シナリオを示すサンプルを示します。

## <a name="samples-and-additional-resources"></a>サンプルと追加のリソース

- [サンプル アプリケーション](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/LocalMediaSamples)
- [Graph SDK ドキュメントの呼び出し](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/)

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [サポートされているメディア形式](~/resources/media-formats.md)
