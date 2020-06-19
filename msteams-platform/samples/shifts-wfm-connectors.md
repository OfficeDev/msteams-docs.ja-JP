---
title: Teams でコネクタをシフトする
description: 要員管理は、Teams のコネクタをシフト
author: laujan
ms.date: 03/09/2020
keywords: Microsoft Teams コネクタ kronos
ms.author: lajanuar
ms.openlocfilehash: eae88d02647f0547eed53d8bd5e00e13a8e62096
ms.sourcegitcommit: 058b7bbd817af5f513e0e018f2ef562dc3086a84
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/03/2020
ms.locfileid: "44801297"
---
# <a name="microsoft-teams-shifts-wfm-connectors"></a>Microsoft Teams が WFM コネクタをシフトする  

## <a name="workforce-management-connectors-wfm-for-firstline-workers"></a>第一線ワーカーの労働力管理コネクタ (wfm) 

Teams は、wfm コネクタをシフトする、運用の準備が整っているオープンソースであり、コミュニティによる統合による統合を提供しています。これは、チームがシフトしてくる第一線ワーカーのデジタル変換に対して、シームレスな操作と迅速なプロセスを提供します。 

各コネクタは、組織への展開と統合に関する詳細なガイダンスを提供します。 完全なソースコードは、詳細に調査したり、特定のニーズに合わせて調整したりできる、GitHub リポジトリで利用できます。

## <a name="key-benefits-teams-shifts-wfm-connectors"></a>主な利点: Teams での WFM コネクタのシフト

* **プラグアンドプレイの操作。** すべてのシフトの WFM コネクタには、Microsoft Azure で必要なすべてのサービスをホストできる ARM Azure 展開スクリプトが含まれています。 アプリを展開するためのコーディングは必要ありません。

* **運用可能なコード。** すべてのシフトコネクタは、推奨されるセキュリティとインフラストラクチャのベストプラクティスに準拠しており、コミュニティで提出されたすべての変更を確認して、引き続き準拠するようにします。

* **カスタマイズと拡張。**  すべてのシフトがすぐに使用できるように展開する準備が整っていますが、コードベースと展開スクリプト全体が提供されるので、独自のニーズに合わせてカスタマイズまたは拡張することが容易になります。

* **詳細なドキュメント & サポート。**  すべてのシフトの WFM コネクタには、ソリューションのアーキテクチャ、展開、および構成手順に関するエンドツーエンドのドキュメントが付属しています。 コネクタリポジトリは監視されるので、リポジトリの GitHub 問題追跡ツールを使用して発生した問題、課題、または問題を報告してください。

* **シームレスな統合。** Wfm ソリューションと teams のシフトを統合することで、第一線ワーカーは teams の交代アプリを使用して、自分のスケジュールとシフト時間を表示/管理し、別のアプリにコンテキストを切り替えることなく、自分のモバイルデバイスやデスクトップから teams で提供されている他のすべてのコラボレーション機能を使用することができます。

**Teams でのシフトビューを開く**  
![Teams でのオープンシフト](../assets/images/teams-open-shifts-view.png)

## <a name="kronos-to-teams-shifts-connector"></a>Kronos-Teams シフトコネクタ

オープンソースコードでは、次の最初の行のワーカーおよびマネージャーのシナリオについて Teams の移行 (デスクトップ/モバイル Teams アプリ) を使用して、Kronos 労働力の中央バージョン8.1 以降を統合することができます。

1. スケジュールを表示します。

1. 公開して、オープンシフトを要求します。

1. 切り替えを行います。

1. 要求時間がオフになっています。

1. シフトを提供します。

[GitHub で取得する]( https://aka.ms/KronosShiftsConnector)

## <a name="jda-to-teams-shifts-connector"></a>JDA-Teams シフトコネクタ

オープンソースコードでは、JDA (BlueYonder) バージョン17.2 以降を統合できます。この場合、次の最初の行のワーカーおよびマネージャーのシナリオについて Teams の交代 (デスクトップ/モバイル Teams アプリ) を使用します。

1. JDA の移動とスケジュールグループを発行し、Teams で表示します。

1. シフトの切り替えや休暇の要求など、高度なスケジュールシナリオを有効にします。

1. [Microsoft GRAPH API](/graph/api/resources/shift?view=graph-rest-beta)を使用して、ユーザーの可用性をシフトに設定します。

[GitHub で取得する](https://aka.ms/JDAShiftsConnector)</br></br>
