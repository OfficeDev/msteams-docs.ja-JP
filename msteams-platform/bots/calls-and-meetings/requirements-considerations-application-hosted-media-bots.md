---
title: アプリケーションでホストされるメディア ボットの要件と考察
description: コード例とサンプルを使用して、Microsoft Teams 用のアプリケーションでホストされるメディア ボットの作成に関連する重要な要件と考慮事項、およびスケーラビリティとパフォーマンスに関する考慮事項について説明します。
ms.topic: conceptual
ms.localizationpriority: medium
keywords: アプリケーションでホストされるメディア Windows Server Azure VM
ms.date: 11/16/2018
ms.openlocfilehash: 987bb26ba7ad91f11228f7072d3e268ebd87dc5a
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2022
ms.locfileid: "65756612"
---
# <a name="requirements-and-considerations-for-application-hosted-media-bots"></a>アプリケーションでホストされるメディア ボットの要件と考察

アプリケーションでホストされるメディア ボットでは、オーディオおよびビデオ メディア ストリームにアクセスするために [`Microsoft.Graph.Communications.Calls.Media` .NET ライブラリ](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/)が必要です。このボットは、Windows Server オンプレミス マシンまたは Azure の Windows Server ゲスト オペレーティング システム (OS) にデプロイする必要があります。

> [!NOTE]
>
> * メッセージング ボットや対話型音声応答 (IVR) ボットの開発に関するガイダンスは、アプリケーションでホストされるメディア ボットの構築には完全には適用されません。
> * Microsoft Real-Time Media Platform for Bots は開発者向けプレビュー段階であるため、このドキュメントのガイダンスは変更される可能性があります。

## <a name="c-or-net-and-windows-server-for-development"></a>開発用の C# または .NET および Windows Server

アプリケーションでホストされるメディア ボットには、次のものが必要です。

* ボットは C# と標準の.NET Framework で開発し、Microsoft Azure にデプロイする必要があります。 C++ または Node.js API を使用してリアルタイム メディアにアクセスすることはできません。また、.NET Core はアプリケーションでホストされるメディア ボットではサポートされていません。

* このボットは、次のいずれかの Azure サービス環境内でホストできます。
  * クラウド サービス。
  * Virtual Machine Scale Sets (VMSS) を使用した Service Fabric。
  * サービスとしてのインフラストラクチャ (IaaS) 仮想マシン (VM)。  
  
* このボットは、Azure Web アプリとしてデプロイすることはできません。

* このボットは、最新バージョンの `Microsoft.Graph.Communications.Calls.Media` .NET ライブラリで実行されている必要があります。 このボットは、使用可能な最新バージョンの [NuGet パッケージ](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/)か、3 か月以下のバージョンを使用する必要があります。 以前のバージョンのライブラリは非推奨となり、数か月後には機能しません。 `Microsoft.Graph.Communications.Calls.Media` ライブラリを最新の状態に保つことで、ボットと Microsoft Teams の間の最適な相互運用性を確保できます。

次のセクションでは、リアルタイム メディア呼び出しがどこに存在するかについて詳しく説明します。

## <a name="real-time-media-calls-stay-where-theyre-created"></a>リアルタイム メディア呼び出しは、作成された場所に留まる

リアルタイム メディア呼び出しは、その呼び出しが作成されたコンピューターに留まります。 リアルタイム メディア呼び出しは、呼び出しを受け入れたか開始した仮想マシン (VM) インスタンスにピン留めされます。 Microsoft Teams 呼び出しまたは会議フローからその VM インスタンスへのメディアと、ボットが Microsoft Teams に返送するメディアも、その VM から発信される必要があります。 その VM が停止されたときに処理中のリアルタイム メディア呼び出しがある場合、それらの呼び出しは突然終了します。 保留中の VM シャットダウンに関する予備知識をボットが持っている場合は、ボットが呼び出しを終了できます。

次のセクションでは、アプリケーションでホストされるメディア ボットのアクセシビリティについて詳しく説明します。

## <a name="application-hosted-media-bots-accessible-on-the-internet"></a>インターネット上でアクセス可能なアプリケーションでホストされるメディア ボット

アプリケーションでホストされるメディア ボットは、インターネット上で直接アクセスできる必要があります。 これらのボットには、次の機能が含まれている必要があります。

* アプリケーションでホストされるメディア ボットを Azure でホストしている各 VM インスタンスには、インスタンス レベルのパブリック IP アドレス (ILPIP) を使用してインターネットから直接アクセスできる必要があります。
  * Azure クラウド サービス用の ILPIP を取得して構成する方法については、「[インスタンス レベル パブリック IP (クラシック) の概要](/azure/virtual-network/virtual-networks-instance-level-public-ip)」を参照してください。
  * VM スケール セット用の ILPIP を構成する方法については、「[仮想マシンごとのパブリック IPv4](/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-networking#public-ipv4-per-virtual-machine)」を参照してください。
* アプリケーションでホストされるメディア ボットをホストしているサービスでは、特定のインスタンスにマップされる公開ポートを使用して各 VM インスタンスを構成する必要もあります。
  * Azure クラウド サービスの場合、これにはインスタンス入力エンドポイントが必要です。 詳細については、[Azure でロール インスタンスの通信を有効にする](/azure/cloud-services/cloud-services-enable-communication-role-instances)方法に関する記事を参照してください。
  * VM スケール セットの場合は、ロード バランサーに関する NAT 規則を構成する必要があります。 詳細については、「[Azure における仮想ネットワークと仮想マシン](/azure/virtual-machines/windows/network-overview)」を参照してください。

* アプリケーションでホストされるメディア ボットは、Bot Framework Emulator ではサポートされていません。

次のセクションでは、アプリケーションでホストされるメディア ボットのスケーラビリティとパフォーマンスに関する考慮事項について詳しく説明します。

## <a name="scalability-and-performance-considerations"></a>スケーラビリティとパフォーマンスに関する検討事項

アプリケーションでホストされるメディア ボットには、次のスケーラビリティとパフォーマンスに関する考慮事項が必要です。

* アプリケーションでホストされるメディア ボットでは、メッセージング ボットよりも多くのコンピューティングとネットワーク (帯域幅) の容量が必要であり、運用コストが高くなる可能性があります。 リアルタイム メディア ボット開発者は、ボットのスケーラビリティを慎重に測定し、ボットが管理できるよりも多くの同時呼び出しを受け入れないようにする必要があります。 ビデオ対応ボットでは、CPU コアあたり 1 つか 2 つの同時メディア セッションしか維持できない可能性があります ("RAW" RGB24 または NV12 ビデオ形式を使用している場合)。
* Real-time Media Platform は、現時点では、H.264 ビデオ エンコード/デコードをオフロードするために VM で使用可能なグラフィックス処理装置 (GPU) を利用することはしていません。 代わりに、ビデオのエンコードとデコードは、CPU 上のソフトウェアで行われます。 GPU が使用可能な場合、ボットは独自のグラフィックス レンダリングにその GPU を利用できます (ボットが 3D グラフィックス エンジンを使用している場合など)。
* リアルタイム メディア ボットをホストしている VM インスタンスには、少なくとも 2 つの CPU コアが必要です。 Azure の場合は、Dv2 シリーズの仮想マシンをお勧めします。 その他の Azure VM の種類では、4 つの仮想 CPU (vCPU) を備えたシステムが必要な最小サイズです。 Azure VM の種類の詳細については、[Azure のドキュメント](/azure/virtual-machines/windows/sizes-general)を参照してください。

## <a name="code-sample"></a>コード サンプル

アプリケーションでホストされるメディア ボットのサンプルは次のとおりです。

| **サンプルの名前** | **説明** | **Graph** |
|------------|-------------|-----------|
| ローカル メディアのサンプル | さまざまなローカル メディア シナリオを示すサンプル。 | [表示](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/LocalMediaSamples) |
| リモート メディアのサンプル | さまざまなリモート メディア シナリオを示すサンプル。 | [表示](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/RemoteMediaSamples) |

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [サポートされているメディア形式](~/resources/media-formats.md)

## <a name="see-also"></a>関連項目

* [Graph 呼び出し SDK に関するドキュメント](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/)
* ボットには、メッセージング ボットよりも多くのコンピューティングとネットワーク帯域幅の容量が必要であり、運用コストが高くなります。 リアルタイム メディア ボット開発者は、ボットのスケーラビリティを慎重に測定し、ボットが管理できるよりも多くの同時呼び出しを受け入れないようにする必要があります。 RAW RGB24 または NV12 ビデオ形式を使用している場合、ビデオ対応ボットでは、CPU コアあたり 1 つか 2 つの同時メディア セッションしか維持できません。
* リアルタイム メディア プラットフォームでは、現在、H.264 ビデオ エンコードまたはデコードをオフロードするために VM で使用可能なグラフィックス処理装置 (GPU) を利用していません。 代わりに、ビデオのエンコードとデコードは、CPU 上のソフトウェアで行われます。 GPU が使用可能な場合、ボットは独自のグラフィックス レンダリングにその GPU を利用します (ボットが 3D グラフィックス エンジンを使用している場合など)。
* リアルタイム メディア ボットをホストしている VM インスタンスには、少なくとも 2 つの CPU コアが必要です。 Azure の場合は、Dv2 シリーズの仮想マシンをお勧めします。 その他の Azure VM の種類では、4 つの仮想 CPU (vCPU) を備えたシステムが必要な最小サイズです。 Azure VM の種類の詳細については、[Azure のドキュメント](/azure/virtual-machines/windows/sizes-general)を参照してください。

次のセクションでは、さまざまなローカル メディアシナリオを示すサンプルを提供します。

## <a name="samples-and-additional-resources"></a>サンプルとその他のリソース

* [サンプル アプリケーション](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/LocalMediaSamples)
* [Graph 呼び出し SDK に関するドキュメント](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/)
