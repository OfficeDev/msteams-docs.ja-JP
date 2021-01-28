---
title: Teams シフト コネクタ
description: Teams の従業員管理シフト コネクタ
ms.topic: reference
author: laujan
ms.date: 03/09/2020
keywords: Microsoft Teams コネクタ kronos
ms.author: lajanuar
ms.openlocfilehash: 9d32c9e1aa3baba660440492df55bb00f677baa4
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014594"
---
# <a name="microsoft-teams-shifts-wfm-connectors"></a>Microsoft Teams が WFM コネクタをシフトする  

## <a name="workforce-management-connectors-wfm-for-firstline-workers"></a>ファーストライン ワーカー用の要員管理コネクタ (WFM) 

Teams シフト WFM コネクタは、Teams シフトによるファーストライン ワーカーのデジタル変換のためのシームレスなエクスペリエンスと迅速なプロセスを提供する、実稼働対応、オープン ソース、およびコミュニティ駆動型の統合です。 

各コネクタは、組織への展開と統合に関する詳細なガイダンスを提供します。 完全なソース コードは、GitHub リポジトリで入手できます。このリポジトリでは、特定のニーズに合わせて詳細に探索したり、フォークしたり、カスタマイズすることができます。

## <a name="key-benefits-teams-shifts-wfm-connectors"></a>主な利点: Teams が WFM コネクタをシフトする

* **プラグ アンド プレイ エクスペリエンス。** すべての Shifts WFM コネクタには、必要ARMサービスを Microsoft Azure でホストできる Azure 展開スクリプトが含まれています。 アプリを展開するためにコーディングは必要ありません。

* **実稼働対応のコード。** すべてのシフト コネクタは推奨されるセキュリティとインフラストラクチャのベスト プラクティスに準拠し、コミュニティから提出された変更はすべて、継続的に準拠するためにレビューされます。

* **カスタマイズ可能で拡張可能。**  すべての Shifts WFM コネクタは、すぐに使用するために展開できる状態ですが、独自のニーズに合わせて簡単にカスタマイズまたは拡張できるよう、コード ベースと展開スクリプト全体が用意されています。

* **サポートに関する&ドキュメント。**  すべての Shifts WFM コネクタには、ソリューションのアーキテクチャ、展開、および構成の手順に関するエンドツーエンドのドキュメントが付属しています。 コネクタ リポジトリは監視されます。そのため、リポジトリの GitHub の問題追跡ツールを使用して、発生した問題、課題、または困難を報告してください。

* **シームレスな統合。** WFM ソリューションと Teams シフトの統合により、ファーストライン ワーカーは Teams シフト アプリを使用してスケジュールとシフト タイムを表示/管理し、Teams で提供されるその他すべての豊富なコラボレーション機能をモバイル デバイスやデスクトップから使用できます。コンテキストを別のアプリに切り替える必要が生じることなく、Teams で提供されます。

**Teams でシフト ビューを開く**  
![Teams でシフトを開く](../assets/images/teams-open-shifts-view.png)

## <a name="kronos-to-teams-shifts-connector"></a>Kronos から Teams へのシフト コネクタ

オープン ソース コードを使用すると、Kronos Workforce Central Version 8.1 以上を Teams シフト (デスクトップ/モバイル Teams アプリ) と統合して、次のファーストライン ワーカーおよびマネージャー シナリオに対応できます。

1. スケジュールを表示します。

1. オープン シフトを公開して要求します。

1. スワップ シフト。

1. 要求のタイム オフ。

1. シフトを提供します。

[GitHub で入手する]( https://aka.ms/KronosShiftsConnector)

## <a name="jda-to-teams-shifts-connector"></a>JDA から Teams へのシフト コネクタ

オープン ソース コードを使用すると、JDA (BlueYonder) バージョン 17.2 以上を Teams シフト (デスクトップ/モバイル Teams アプリ) と統合して、次のファーストライン ワーカーおよびマネージャー シナリオに対応できます。

1. JDA でシフトを公開し、グループをスケジュールし、Teams で表示します。

1. シフト スワップの要求やタイム オフなど、豊富なスケジュールシナリオを有効にします。

1. シフト用 Microsoft [Graph API を使用してユーザーの可用性を設定します](/graph/api/resources/shift?view=graph-rest-beta) 。

[GitHub で入手する](https://aka.ms/JDAShiftsConnector)</br></br>
