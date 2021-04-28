---
title: 本番対応の Shifts コネクタ
description: Workforce management Shifts connectors for Teams
ms.topic: reference
author: laujan
ms.date: 03/09/2020
localization_priority: Normal
keywords: Microsoft Teams コネクタ kronos
ms.author: lajanuar
ms.openlocfilehash: d17e3e18cfd39fec8117ce46aa99cb99da6927bc
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058699"
---
# <a name="production-ready-shifts-connectors"></a>本番対応の Shifts コネクタ  

Teams Shifts Workforce Management (WFM) コネクタは、運用対応、オープン ソース、コミュニティ駆動型の統合であり、ファーストラインワーカーに役立ちます。 Teams Shifts を使用したファーストライン ワーカーのデジタル変換のためのシームレスなエクスペリエンスと迅速なプロセスを提供します。 

各コネクタは、組織への展開と統合に関する詳細なガイダンスを提供します。 完全なソース コードは GitHub リポジトリで使用できます。 詳細またはフォークを探索し、特定のニーズに合わせてカスタマイズできます。   

このドキュメントでは、Teams Shifts WFM コネクタ、Kronos-to-Teams Shifts コネクタ、および JDA 間 Teams シフト コネクタの主な利点の概要を示します。

## <a name="key-benefits-of-teams-shifts-wfm-connectors"></a>Teams Shifts WFM コネクタの主な利点

Teams Shifts WFM コネクタの主な利点は次のとおりです。

* **プラグ アンド プレイのエクスペリエンス:** すべての Shifts WFM コネクタには、Microsoft Azure ARM必要なすべてのサービスをホストできる Azure 展開スクリプトが含まれています。 アプリを展開するためにコーディングは必要ありません。

* **実稼働可能なコード:** すべての Shifts コネクタは、推奨されるセキュリティとインフラストラクチャのベスト プラクティスに準拠し、コミュニティが提出した変更はすべて確認され、継続的に準拠します。

* **カスタマイズ可能で拡張可能:**  すべての Shifts WFM コネクタは、すぐに使用できるように展開できる状態ですが、コード ベースと展開スクリプト全体をすぐに利用できます。 独自のニーズに合わせて簡単にカスタマイズまたは拡張できます。

* **サポートに関する&ドキュメント:**  すべての Shifts WFM コネクタには、ソリューションのアーキテクチャ、展開、および構成手順に関するエンドツーエンドのドキュメントが付属しています。 コネクタ リポジトリは監視され、リポジトリの GitHub Issues トラッカーを通じて発生する問題、課題、または困難を報告できます。

* **シームレスな統合:** WFM ソリューションと Teams Shifts の統合により、ファーストラインワーカーは Teams Shifts アプリを使用してスケジュールとシフト時間を表示または管理し、Teams で提供されるその他の豊富なコラボレーション機能をモバイル デバイスまたはデスクトップから別のアプリに切り替えることなく使用できます。  

**Teams でシフト ビューを開く** 

Teams のシフト ビューを次の図に示します。 

![Teams でシフトを開く](../assets/images/teams-open-shifts-view.png)

## <a name="kronos-to-teams-shifts-connector"></a>Kronos-to-Teams Shifts コネクタ

オープンソース コードを使用すると、Kronos Workforce Central Version 8.1 以上を、次のファーストライン ワーカーおよびマネージャー シナリオ用のデスクトップまたはモバイル Teams アプリなどの Teams Shifts と統合できます。

* スケジュールを表示します。

* オープン シフトを発行して要求します。

* スワップ シフト。

* 要求の時間を指定します。

* シフトを提供します。

Kronos-to-Teams Shifts コネクタの展開の詳細については [、「Get it on GitHub」を参照してください](https://aka.ms/KronosShiftsConnector)。

## <a name="jda-to-teams-shifts-connector"></a>JDA から Teams へのシフト コネクタ

オープンソース コードを使用すると、BlueYonder バージョン 17.2 以上などの JDA を、次のファーストライン ワーカーおよびマネージャー シナリオ用のデスクトップまたはモバイル Teams アプリなどの Teams シフトと統合できます。

* JDA でシフトとスケジュール グループを発行し、Teams で表示します。

* シフト スワップの要求やタイム オフを含む、豊富なスケジュール設定シナリオを有効にします。

* Microsoft Graph API for [Shifts を使用してユーザーの可用性を設定します](/graph/api/resources/shift?view=graph-rest-beta&preserve-view=true)。

投稿と提案の詳細については [、「Get it on GitHub」を参照してください](https://aka.ms/JDAShiftsConnector)。</br></br>

## <a name="see-also"></a>関連項目

- [Web アプリを統合する](~/samples/integrate-web-apps-overview.md)
