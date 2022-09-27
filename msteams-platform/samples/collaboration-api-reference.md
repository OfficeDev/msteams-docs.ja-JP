---
title: コラボレーションコントロールと設定 REST API リファレンス
author: surbhigupta
description: このモジュールでは、設定の管理、開始、マッピング、およびコラボレーション アクティビティの取得を行うコラボレーションコントロールと設定 REST API リファレンスについて説明します。
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: 7a990cf23d0832e26a9d8bc6ef9dc2f34ea06a53
ms.sourcegitcommit: c1032ea4f48c4bbf5446798ff7d46d7e6e9f55d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2022
ms.locfileid: "68027299"
---
# <a name="collaboration-control-and-settings-rest-api-reference"></a>コラボレーションコントロールと設定 REST API リファレンス

開発者は、コラボレーション コントロールと設定 REST API を使用して、独自のビジネス モデル エンティティを使用して、設定の管理、開始、マッピング、およびコラボレーション アクティビティの取得を行うことができます。

> [!NOTE]
> 現在、コラボレーション コントロールは [、パブリック開発者向けプレビュー](~/resources/dev-preview/developer-preview-intro.md)でのみ使用できます。

この記事では、コラボレーション コントロール ソリューション REST API のリファレンスを提供します。

## <a name="rest-operations-collaboration---custom-api"></a>REST 操作: コラボレーション - カスタム API

|操作​​|説明|
|---------|-----------|
|[コラボレーション マップの関連付け](/rest/api/industry/collaboration-controls/collaboration-custom-ap-is/associate-collaboration-map)|コラボレーション エンティティをコラボレーション セッションに関連付けます。|
|[コラボレーション セッションの開始](/rest/api/industry/collaboration-controls/collaboration-custom-ap-is/begin-collaboration-session)|ビジネス エンティティ、アプリケーション コンテキスト、およびオプションのメタデータにリンクされたコラボレーション セッション レコードを作成します。|
|[コラボレーション マップの関連付けを解除する](/rest/api/industry/collaboration-controls/collaboration-custom-ap-is/disassociate-collaboration-map-custom-api)|特定のコラボレーション セッションからマップされたエンティティの関連付けを解除します。|
|[コラボレーション マップを取得する](/rest/api/industry/collaboration-controls/collaboration-custom-ap-is/retrieve-collaboration-maps-custom-api)|特定のエンティティ型のセッションのコラボレーション マップの一覧を取得します。|
|[コラボレーション セッションの取得](/rest/api/industry/collaboration-controls/collaboration-custom-ap-is/retrieve-collaboration-session-custom-api)|指定されたパラメーターに基づいてコラボレーション セッション レコードを取得します。|
|[コラボレーション マップを更新する](/rest/api/industry/collaboration-controls/collaboration-custom-ap-is/update-collaboration-map-custom-api)|コラボレーション マップ レコードとそのメタデータを更新します (指定されている場合)。|
|[コラボレーション セッションの更新](/rest/api/industry/collaboration-controls/collaboration-custom-ap-is/update-collaboration-session)|コラボレーション セッション レコードと必要に応じてそのメタデータを更新します。|

## <a name="rest-operations-collaboration---standard-odata-apis"></a>REST 操作: コラボレーション - Standard OData API

|操作​​|説明|
|---------|-----------|
|[Id でコラボレーション マップを取得する](/rest/api/industry/collaboration-controls/collaboration-standard-o-data-ap-is/get-collaboration-map-by-id)|コラボレーション マップ レコードから詳細を取得します。|
|[コラボレーション メタデータを取得する](/rest/api/industry/collaboration-controls/collaboration-standard-o-data-ap-is/get-collaboration-metadata)|特定のコラボレーション マップまたはコラボレーション ルート エンティティ名のコラボレーション メタデータ レコードの一覧を取得します。|
|[コラボレーション ルートを取得する](/rest/api/industry/collaboration-controls/collaboration-standard-o-data-ap-is/get-collaboration-root)|作成されたすべてのコラボレーション セッションを一覧表示します。|

## <a name="rest-operations-settings---custom-apis"></a>REST 操作: 設定 - カスタム API

|操作​​|説明|
|---------|-----------|
|[設定の作成と更新](/rest/api/industry/collaboration-controls/settings-custom-ap-is/create-update-setting-custom-api)|グループ パスと設定定義名の両方に一致する設定を作成または更新します。|
|[Null 設定を取得する](/rest/api/industry/collaboration-controls/settings-custom-ap-is/retrieve-null-settings-custom-api)|値を持たない設定定義の一覧を返します。|
|[設定を取得する](/rest/api/industry/collaboration-controls/settings-custom-ap-is/retrieve-settings-custom-api)|グループ内の特定の設定または設定の一覧を返します。|

## <a name="rest-operations-settings---standard-odata-apis"></a>REST 操作: 設定 - Standard OData API

|操作​​|説明|
|---------|-----------|
|[設定定義の削除](/rest/api/industry/collaboration-controls/settings-standard-o-data-ap-is/delete-settings-definition)|設定定義を削除します。|
|[設定グループの削除](/rest/api/industry/collaboration-controls/settings-standard-o-data-ap-is/delete-settings-group)|設定グループを削除します。|
|[設定の種類の削除](/rest/api/industry/collaboration-controls/settings-standard-o-data-ap-is/delete-settings-type)|設定の種類を削除します。|
|[[設定の削除] の値](/rest/api/industry/collaboration-controls/settings-standard-o-data-ap-is/delete-settings-value)|設定値を削除します。|
|[設定定義を取得する](/rest/api/industry/collaboration-controls/settings-standard-o-data-ap-is/get-settings-definitions)|設定の定義を一覧表示します。|
|[設定グループを取得する](/rest/api/industry/collaboration-controls/settings-standard-o-data-ap-is/get-settings-groups)|設定グループを一覧表示します。|
|[設定の種類を取得する](/rest/api/industry/collaboration-controls/settings-standard-o-data-ap-is/get-settings-types)|設定の種類を一覧表示します。|
|[設定の値を取得する](/rest/api/industry/collaboration-controls/settings-standard-o-data-ap-is/get-settings-value)|設定の値を一覧表示します。|
|[パッチ設定の定義](/rest/api/industry/collaboration-controls/settings-standard-o-data-ap-is/patch-settings-definition)|設定定義を更新します。|
|[パッチ設定グループ](/rest/api/industry/collaboration-controls/settings-standard-o-data-ap-is/patch-settings-group)|設定グループを更新します。|
|[パッチ設定の種類](/rest/api/industry/collaboration-controls/settings-standard-o-data-ap-is/patch-settings-type)|設定の種類を更新します。|
|[パッチ設定の値](/rest/api/industry/collaboration-controls/settings-standard-o-data-ap-is/patch-settings-value)|設定値を更新します。|
|[Post Settings Definition](/rest/api/industry/collaboration-controls/settings-standard-o-data-ap-is/post-settings-definition)|新しい設定定義を作成します。|
|[Post Settings Group](/rest/api/industry/collaboration-controls/settings-standard-o-data-ap-is/post-settings-group)|新しい設定グループを作成します。|
|[Post Settings Type](/rest/api/industry/collaboration-controls/settings-standard-o-data-ap-is/post-settings-type)|新しい設定の種類を作成します。|
|[Post Settings Value](/rest/api/industry/collaboration-controls/settings-standard-o-data-ap-is/post-settings-value)|新しい設定値を作成します。|
