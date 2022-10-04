---
title: コラボレーション コントロール
author: surbhigupta
description: このモジュールでは、コラボレーション コントロールを使用して、Planner、Bookings、Outlook などの Microsoft 365 サービスと統合するアプリを作成する方法について説明します。
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: fa0cb45921820a61fbfd7112a50f28eb9230fb4b
ms.sourcegitcommit: f2ac771cbd608e872604e9ac8ffec2d08f55ee1a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2022
ms.locfileid: "68373025"
---
# <a name="collaboration-controls"></a>コラボレーション コントロール

コラボレーション コントロールを使用すると、Microsoft 365 と Microsoft Teams for Approvals、Files、Meetings、Notes、Tasks を適用して、ビジネス プロセスに関するコンテキスト コラボレーションを有効にすることができます。 これらのコントロールを使用すると、Teams で直接表示できるカスタムコラボレーション エクスペリエンスを構築できます。 コラボレーション コントロールを構成するソリューションにより、メーカーは、Planner、Bookings、Outlook、SharePoint などの Microsoft 365 サービスと統合するアプリケーションを低コードで構築できます。

これらのコントロールを使用すると、ビジネス アプリのラインを構築し、次のコンテキストをアプリからアプリに切り替えることなく作業することで、ユーザーのワークフロー コラボレーションを簡略化する機能が提供されます。

* 承認
* Files
* 会議
* メモ
* タスク

> [!NOTE]
> 現在、コラボレーション コントロールは [、パブリック開発者向けプレビュー](~/resources/dev-preview/developer-preview-intro.md)でのみ使用できます。

コラボレーション コントロールの主な機能の一部を次に示します。

* **Microsoft Planner タスク:** タスクを作成し、レコードのメンバーに割り当てて、Microsoft Teams のモデル駆動型アプリとタスク アプリのタスクの統合リストを表示できるようにします。

* **Dataverse タスク:** 組織の外部にいるユーザーに割り当てることができるタスクを作成します。

* **Dataverse Notes:** アプリ内のレコードに割り当てられているメモを作成します。

* **Outlook 会議:** 顧客と社内の従業員の両方との会議をスケジュールし、Microsoft Teams で他のユーザーとシームレスに接続し、ボタンを選択します。

* **SharePoint ファイル:** SharePoint に支えられた一元的な場所で関連する成果物を検索、参照、編集できるように、レコードのメンバーとファイルを共有します。

* **承認：** チーム内の要求を効率化します。

> [!NOTE]
> 前に説明したコラボレーション コントロールのさまざまな Microsoft 365 機能を構成して使用することで、ユーザー データがGraph APIを通過し、[Microsoft API 利用規約](/legal/microsoft-apis/terms-of-use?context=graph%2Fcontext)に同意するためのアクセス許可が付与されます。 詳細については、 [Microsoft Graph](/graph/overview) に関するページを参照してください。

## <a name="how-collaboration-controls-works"></a>コラボレーション コントロールのしくみ

コントロールは、Microsoft Teams に展開できる Power Apps モデル 駆動型アプリケーション (MDA) 内で実行されます。 MDA は Microsoft Dataverse で実行され、カスタム データ モデルと統合できます。 コントロールは、Planner タスク、Outlook と Teams の予定表、SharePoint ファイル用の Microsoft Graph と統合されます。 コラボレーション コントロールは、レコードのシステムやポータルなどの外部ソースと直接統合されません。

* データは、標準の OData API を使用して外部ソースから Dataverse に追加できます。

* データは、標準の OData API を使用して Dataverse から読み取り、レコードのシステムやポータルなどの外部ソースに送信できます。

:::image type="content" source="~/assets/images/collaboration-control/consumption-mda.png" alt-text="コラボレーションのライフサイクル":::
