---
title: コラボレーション コントロール
author: surbhigupta
description: このモジュールでは、コラボレーション コントロールを使用して、Planner、Bookings、Outlook などの Microsoft 365 サービスと統合するアプリを作成する方法について説明します。
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: cd35cc3b1f9340581bb45a2c9eb707793e044736
ms.sourcegitcommit: 0bb822b30739e4a532a36764dad2dbf35a81ba29
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2022
ms.locfileid: "67179267"
---
# <a name="collaboration-controls"></a>コラボレーション コントロール

コラボレーション コントロールを使用すると、承認、ファイル、会議、メモ、タスクに Microsoft 365 とMicrosoft Teamsを適用して、ビジネス プロセスに関するコンテキスト コラボレーションを有効にすることができます。 これらのコントロールを使用すると、Teams で直接表示できるカスタムコラボレーション エクスペリエンスを構築できます。 コラボレーション コントロールを構成するソリューションにより、メーカーは、Planner、Bookings、Outlook、SharePoint などの Microsoft 365 サービスと統合するアプリケーションを低コードで構築できます。

これらのコントロールを使用すると、アプリからアプリにコンテキストを切り替えることなく、承認、ファイル、会議、メモ、タスクを使用して基幹業務アプリを構築することで、ユーザーワークフローコラボレーションを簡略化できます。

> [!NOTE]
> 現在、コラボレーション コントロールは [、パブリック開発者向けプレビュー](~/resources/dev-preview/developer-preview-intro.md)でのみ使用できます。

コラボレーション コントロールの主な機能の一部を次に示します。

* **Microsoft Planner タスク:** タスクを作成し、レコードのメンバーに割り当てて、モデル駆動型アプリとタスク アプリのタスクの統合リストをMicrosoft Teamsで表示できるようにします。

* **Dataverse タスク:** 組織の外部にいるユーザーに割り当てることができるタスクを作成します。

* **Dataverse Notes:** アプリ内のレコードに割り当てられているメモを作成します。

* **Outlook 会議:** 顧客と社内の従業員の両方との会議をスケジュールし、ボタンを選択してMicrosoft Teamsで他のユーザーとシームレスに接続します。

* **SharePoint ファイル:** SharePoint に支えられた一元的な場所で関連する成果物を検索、参照、編集できるように、レコードのメンバーとファイルを共有します。

* **承認：** チーム内の要求を効率化します。

> [!NOTE]
> 上記のコラボレーション コントロールのさまざまな Microsoft 365 機能を構成して使用することで、ユーザー データがGraph APIを通過し、[Microsoft API の使用条件](/legal/microsoft-apis/terms-of-use?context=graph%2Fcontext)に同意するためのアクセス許可が付与されます。 詳細については、 [Microsoft Graph](/graph/overview) に関するページを参照してください。

## <a name="how-collaboration-controls-works"></a>コラボレーション コントロールのしくみ

コントロールは、Microsoft Teamsにデプロイできる Power Apps モデル 駆動型アプリケーション [MDA] 内で実行されます。 MDA は Microsoft Dataverse で実行され、カスタム データ モデルと統合できます。 コントロールは、Planner タスク、Outlook と Teams の予定表、SharePoint ファイル用の Microsoft Graph と統合されます。 コラボレーション コントロールは、レコードのシステムやポータルなどの外部ソースと直接統合されません。

* データは、標準の OData API を使用して外部ソースから Dataverse に追加できます。

* データは、標準の OData API を使用して Dataverse から読み取り、レコードのシステムやポータルなどの外部ソースに送信できます。

:::image type="content" source="~/assets/images/collaboration-control/consumption-mda.png" alt-text="コラボレーションのライフサイクル":::
