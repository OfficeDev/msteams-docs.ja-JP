---
title: 本番対応の Shifts コネクタ
description: kronos-to-Teams Shifts コネクタや JDA-to-Teams Shifts コネクタなど、Teams 用の Workforce management Shifts コネクタを使用する利点について説明します。
ms.topic: reference
author: surbhigupta
ms.date: 03/09/2020
ms.localizationpriority: medium
keywords: Microsoft Teams コネクタ kronos
ms.author: lajanuar
ms.openlocfilehash: 21ea28e3b5d53226a2ab50ac22db31fef561596a
ms.sourcegitcommit: 2fdca6fb0ade3f6b460eb9a4dfea0a8e2ab8d3b9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/08/2022
ms.locfileid: "63355742"
---
# <a name="production-ready-shifts-connectors"></a>本番対応の Shifts コネクタ  

Teamsシフトワークフォース管理 (WFM) コネクタは、運用対応、オープンソース、コミュニティ駆動型の統合であり、第一線のワーカーに役立ちます。 シームレスなエクスペリエンスと迅速なプロセスを提供し、第一線で働く従業員のデジタルトランスフォーメーションを迅速にTeamsします。

各コネクタは、組織への展開と統合に関する詳細なガイダンスを提供します。 完全なソース コードは、リポジトリGitHubできます。 詳細またはフォークを探索し、特定のニーズに合わせてカスタマイズできます。

このドキュメントでは、Teams Shifts WFM コネクタ、Kronos-to-Teams Shifts コネクタ、および JDA から Teams Shifts コネクタの主な利点の概要を説明します。

## <a name="key-benefits-of-teams-shifts-wfm-connectors"></a>Shifts WFM コネクタTeams主な利点

Shifts WFM コネクタの主な利点Teams次に示します。

* **プラグ アンド プレイのエクスペリエンス:** すべての Shifts WFM コネクタには、ARMで必要なすべてのサービスをホストできる Azure 展開スクリプトがMicrosoft Azure。 アプリを展開するためにコーディングは必要ありません。

* **実稼働可能なコード:** すべての Shifts コネクタは、推奨されるセキュリティとインフラストラクチャのベスト プラクティスに準拠し、コミュニティが提出した変更はすべて確認され、継続的に準拠します。

* **カスタマイズ可能で拡張可能:** すべての Shifts WFM コネクタは、すぐに使用できるように展開できる状態ですが、コード ベースと展開スクリプト全体をすぐに利用できます。 独自のニーズに合わせて簡単にカスタマイズまたは拡張できます。

* **サポートに関する&ドキュメント:** すべての Shifts WFM コネクタには、ソリューションのアーキテクチャ、展開、および構成手順に関するエンドツーエンドのドキュメントが付属しています。 コネクタ リポジトリが監視され、リポジトリの [問題] トラッカーを通じて発生する問題、課題、またはGitHubできます。

* **シームレスな統合:** WFM ソリューションと Teams Shifts の統合により、第一線のワーカーは、Teams Shifts アプリを使用してスケジュールとシフト時間を表示または管理し、コンテキストを別のアプリに切り替えることなく、Teams で提供される他のすべての豊富なコラボレーション機能をモバイル デバイスまたはデスクトップから使用できます。  

**[シフト] ビューを開Teams**

次の図に、Teamsシフト ビューが表示されます。

![シフトを開Teams](../assets/images/teams-open-shifts-view.png)

## <a name="kronos-to-teams-shifts-connector"></a>Kronos-to-Teams Shifts コネクタ

オープンソース コードを使用すると、Kronos Workforce Central Version 8.1 以上を、デスクトップやモバイル Teams アプリなどの Teams Shifts と統合して、次の第 1 行のワーカーとマネージャーのシナリオに対応できます。

* スケジュールを表示します。

* オープン シフトを発行して要求します。

* スワップ シフト。

* 要求の時間を指定します。

* シフトを提供します。

Kronos-to-Teams Shifts コネクタの展開の詳細については、「[Get it on GitHub」 を参照してください](https://aka.ms/KronosShiftsConnector)。

## <a name="jda-to-teams-shifts-connector"></a>JDA-to-Teams Shifts コネクタ

オープンソース コードを使用すると、BlueYonder バージョン 17.2 以上などの JDA を、デスクトップやモバイル Teams アプリなどの Teams Shifts と統合して、次の第 1 行のワーカーとマネージャーのシナリオに対応できます。

* JDA でシフトとスケジュール グループを発行し、そのグループを Teams。

* シフト スワップの要求やタイム オフを含む、豊富なスケジュール設定シナリオを有効にします。

* [Microsoft Graph API for Shifts を使用してユーザーの可用性を設定します](/graph/api/resources/shift?view=graph-rest-beta&preserve-view=true)。

投稿と提案の詳細については、「[Get it on GitHub」 を参照してください](https://aka.ms/JDAShiftsConnector)。

## <a name="see-also"></a>関連項目

[Web アプリを統合する](~/samples/integrate-web-apps-overview.md)
