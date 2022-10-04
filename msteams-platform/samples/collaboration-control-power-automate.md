---
title: コラボレーション コントロール アプリの Power Automate
author: surbhigupta
description: このモジュールでは、Microsoft Teams のコラボレーション制御アプリの Power Automate と Azure アプリの作成方法について説明します。
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: 975d5fdd923d96ae1daa649795259a05904b6921
ms.sourcegitcommit: f2ac771cbd608e872604e9ac8ffec2d08f55ee1a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2022
ms.locfileid: "68373053"
---
# <a name="power-automate"></a>Power Automate

Power Automate を使用すると、Collaboration Manager アプリケーションのワークフローを自動化できます。 たとえば、新しいレコードの作成時にタスクを自動的に作成します。

コラボレーション制御コネクタを使用すると、開発者は、Microsoft Power Automate、Microsoft Power Apps、Azure Logic アプリの自動化されたワークフローでトリガーまたはアクションによってコラボレーション制御 API にアクセスできます。

> [!NOTE]
> 現在、コラボレーション コントロールは [パブリック開発者向けプレビュー](~/resources/dev-preview/developer-preview-intro.md)でのみ使用できます。

このバージョンでは、コネクタを使用すると、作成者はトリガーを設定できます。

1. コラボレーション セッションが作成されたとき。
1. プランナー タスクが作成または変更されたとき。

また、一連のコラボレーション コントロール API と、フローで呼び出すことができるタスクも含まれています。 コネクタアクションは、ワークフロー ステップの選択で見つかります。 コネクタ自体は、構成可能なオプションを備えたカスタム コネクタにあります。 ソリューションでコネクタを使用するには、フローを実行するために環境から信頼されるAzure アプリを作成する必要があります。

## <a name="create-an-azure-app"></a>Azure アプリを作成する

Azure Active Directory 管理の[Azure portal](https://ms.portal.azure.com/#home)で、次の手順でユーザー アプリケーションを環境に追加するための適切なアクセス許可を持つアカウントにサインインします。

1. Azure portalのホーム ページで、**Azure Active Directory** を選択します。 Azure Active Directory で、[ **追加** ] のドロップダウン リストを選択し、[ **アプリの登録**] を選択します。

   :::image type="content" source="../assets/images/collaboration-control/azure-active-directory-home-portal.png" alt-text="スクリーンショットは、新しいアプリ登録を追加する方法を示す例です。":::

   :::image type="content" source="../assets/images/collaboration-control/new-app-registration.png" alt-text="スクリーンショットは、新しいアプリ登録を追加する方法を示す例です。":::

1. アプリの登録で、アプリケーション名を設定し、Web リダイレクト URI を `https://global.consent.azure-apim.net/redirect`.

   :::image type="content" source="../assets/images/collaboration-control/register-an-application.png" alt-text="スクリーンショットは、アプリケーションを登録する方法を示す例です。":::

1. [暗黙的な付与とハイブリッド フロー] セクションで、アクセス トークンと ID トークンの両方を選択します。

   :::image type="content" source="../assets/images/collaboration-control/authorisation-endpoint-tokens.png" alt-text="スクリーンショットは、トークンと ID トークンを示す例です。":::

1. 左側のウィンドウで [API アクセス許可] を選択し、[ **アクセス許可の追加**] を選択し、 **動的 CRM** アクセス許可を検索します。

   :::image type="content" source="../assets/images/collaboration-control/dynamic-crm.png" alt-text="スクリーンショットは、アクセス許可を追加する方法を示す例です。":::

1. Dynamics CRM を選択した後、アクセス許可で **user_impersonation** を選択してください。

   :::image type="content" source="../assets/images/collaboration-control/admin-consent-required.png" alt-text="スクリーンショットは、チェックボックスuser_impersonationを有効にする方法を示す例です。":::

1. [証明書&シークレット] ページで、 **新しいクライアント シークレット** を追加し、コネクタ セキュリティの設定中に後で使用できるように値を保存します。

   :::image type="content" source="../assets/images/collaboration-control/copy-new-secret-value.png" alt-text="スクリーンショットは、新しいシークレット値をコピーする方法を示す例です。":::

1. アプリケーションの [概要] ページで、 **アプリケーション (クライアント) ID を** コピーし、後でコネクタ のセキュリティを設定するときに使用できるように保存します。

   :::image type="content" source="../assets/images/collaboration-control/application-client-ID.png" alt-text="スクリーンショットは、クライアント ID を保存する方法を示す例です":::

これで、Azure アプリがすべて設定され、環境内でユーザー アプリケーションとして追加する必要があります。

## <a name="add-azure-app-to-power-automate-environment"></a>Power Automate 環境に Azure アプリを追加する

1. Power Apps ポータルを開き、右上隅で **設定** を選択し、**中央管理開きます**。

   :::image type="content" source="../assets/images/collaboration-control/power-apps-interface.png" alt-text="Power apps インターフェイスを示す例をスクリーンショットに示します。":::

1. 管理センターで、左側のウィンドウから **[環境** ] を選択し、コネクタ アプリを追加する環境を一覧から選択します。

   :::image type="content" source="../assets/images/collaboration-control/power-platform-admin-center.png" alt-text="スクリーンショットは、コネクタ アプリを追加する方法を示す例です。":::

1. 環境の詳細ページで、[ **設定]** を選択します。

   :::image type="content" source="../assets/images/collaboration-control/settings-environment.png" alt-text="スクリーンショットは、設定を選択する方法を示す例です。":::

1. [設定の詳細] ページで、[ **ユーザーとアクセス許可** ] セクションを選択し、[ **アプリケーション ユーザー**] を選択します。

   :::image type="content" source="../assets/images/collaboration-control/users-link.png" alt-text="スクリーンショットは、アプリケーション ユーザー のリンクを示す例です。":::

1. [アプリ ユーザー] ページで、[ **+ 新しいアプリ ユーザー**] を選択します。 **[新しいアプリの作成] ユーザー** ウィンドウが表示されます。

   :::image type="content" source="../assets/images/collaboration-control/new-app-user.png" alt-text="スクリーンショットは、新しいアプリ ユーザーを示す例です。":::

1. [ **+ アプリの追加] を選択します**。

   :::image type="content" source="../assets/images/collaboration-control/create-new-app-user.png" alt-text="スクリーンショットは、新しいアプリ ユーザーを作成する方法を示す例です。":::

1. 検索ボックスからアプリを選択し、もう一度 [追加] を選択します。

   :::image type="content" source="../assets/images/collaboration-control/add-app-aad.png" alt-text="スクリーンショットは、Azure Active Directory からアプリを追加する方法を示す例です。":::

アプリが追加されたら、 **ビジネス ユニット** と **セキュリティ ロール** をコネクタ アプリケーションに設定します。 [ **作成** ] を選択すると、アプリが一覧に表示されます。 環境でアプリ ユーザーを設定すると、カスタム コネクタの構成に進むことができます。

## <a name="custom-connector-configuration"></a>カスタム コネクタ構成

1. PowerApps または Power Automate を開き、 **カスタム コネクタ メニューを** 選択します。 コラボレーション コネクタの **編集** を選択します。

   :::image type="content" source="../assets/images/collaboration-control/collaboration-connector.png" alt-text="スクリーンショットは、カスタム コネクタ メニューの編集を選択する方法を示しています。":::
1. [全般情報] タブで、Dynamic 365 インスタンス ドメイン (https:// なし) のアドレスを持つホストを入力します。

   :::image type="content" source="../assets/images/collaboration-control/general-information.png" alt-text="スクリーンショットは、[全般] 情報を示す例です。":::

1. [セキュリティ] タブで、次の入力を入力します。

   * クライアント シークレット: 保存したアプリ シークレットの値を入力に使用します。
   * クライアント ID: Azure アプリ (クライアント ID)。
   * リソース URL: Dynamic 365 インスタンスの URL (`https://org.crm.dynamics.com/`)。
   * スコープ: 上記と同じです。 既定のサフィックス (`https://org.crm.dynamics.com/.default`)。

   :::image type="content" source="../assets/images/collaboration-control/dynamic-365-instance.png" alt-text="スクリーンショットは、Dynamic 365 インスタンスを示す例です。":::

1. [ **コネクタの更新]** を選択して変更を保存し、フローで接続を確立できるようにします。

   :::image type="content" source="../assets/images/collaboration-control/custom-connector.png" alt-text="スクリーンショットは、カスタム コネクタを示す例です。":::

## <a name="how-to-invoke-the-connector"></a>コネクタを呼び出す方法  

トリガーとアクションは、構成可能な入力と出力をワークフロー ステップとして事前に定義します。 トリガーまたはアクションを呼び出すタイミングを定義するための正しい入力および出力構成を使用して、ワークフロー ステップを適切なワークフロー位置に追加します。

  :::image type="content" source="../assets/images/collaboration-control/invoke-the-connector.png" alt-text="スクリーンショットは、コネクタを呼び出す方法を示す例です。":::

### <a name="triggers-and-actions-supported-with-connector"></a>コネクタでサポートされているトリガーとアクション

フロー内では、次のトリガーとアクションがサポートされます。

* **トリガー**

  1. コラボレーション セッションが作成されたとき。

      :::image type="content" source="../assets/images/collaboration-control/colab-session-created-preview.png" alt-text="スクリーンショットは、作成されたコラボレーション セッションを示しています。":::

      **スコープ：** フローをトリガーできる行を制限するスコープ。

      **次のように実行します。** 呼び出し元の接続が使用される手順の実行中のユーザー。

  1. タスクが作成または変更されたとき

      :::image type="content" source="../assets/images/collaboration-control/task-created.png" alt-text="スクリーンショットは、タスクが作成または変更されたことを示す例です。":::

      既定では、トリガー Planner タスクは無効になっており、トリガーされません。 これを有効にするには、テナント管理者が次の手順に従う必要があります。

      1. Power Apps/Collaboration コントロール/設定のパスの下にサポート チケットを作成します。
      1. コラボレーション コネクタに対して環境を有効にし、環境 URL (推奨) または組織 ID を提供することを要求します。  
      1. サポート要求に次のサンプル テキストを追加できます。"環境 URL を有効にする: `url` コラボレーション コネクタ用" です。
      1. サポート チケットを開くには、「[ヘルプとサポートを受ける](/power-platform/admin/get-help-support)」を参照してください

* **アクション**

  1. コラボレーション セッションの開始

      :::image type="content" source="../assets/images/collaboration-control/begin-collab-session.png" alt-text="スクリーンショットは、コラボレーション セッションを開始する方法を示す例です。":::

     このステップ アクションにより、dataverse ビジネス エンティティの新しいコラボレーション セッションが作成されます。

      * **アプリケーション名:** たとえば、関連付けられているアプリケーションの名前は、"ローンのCollaboration Manager" または "クローズド ローン監査のCollaboration Manager" です。
      * **コラボレーション ルート エンティティ名:** たとえば、アプリケーション レコードの種類 (テーブル名) は、ローンアプリケーションのCollaboration Managerに対して "msfi_loanapplication" にすることができます。
      * **コラボレーション ルート エンティティ ID:** 関連付けられたアプリケーション レコードの ID (ローン アプリケーション レコードの ID など)。  

      ***高度なオプション***

      **メタデータ (詳細):** コラボレーション セッションのメタデータを追加します。

        * **OData 型:** 他のキー/値が設定されていて、#Microsoft.Dynamics.CRM.m365_collaborationmetadata と正確に一致する必要がある場合は、このフィールドを指定する必要があります。
        * **キー：** メタデータ属性に関連付けられているキー。
        * **値：** メタデータ属性に関連付けられている値。

  1. コラボレーション セッションの取得

      ::image type="content" source="../assets/images/collaboration-control/retrieve-collab-session.png" alt-text="スクリーンショットは、コラボレーション セッションを取得する方法を示す例です。:::

     このステップ アクションは、指定された入力と一致するコラボレーション セッションを返します。

     * **アプリケーション名:** コラボレーション セッションのアプリケーション名コンテキスト。
     * **コラボレーション ルート エンティティ ID:** コラボレーション セッションのビジネス エンティティ ID。  
     * **コラボレーション ルート エンティティ名:** コラボレーション セッションのビジネス エンティティの種類。

  1. コラボレーション セッションの更新

      :::image type="content" source="../assets/images/collaboration-control/update-collab-session.png" alt-text="スクリーンショットは、コラボレーション セッションを更新する方法を示す例です。":::

     このステップ アクションは、既存のコラボレーション セッションを更新します。

     * **コラボレーション ルート ID:** ターゲット コラボレーション セッション/ルート レコードの GUID。
     * **コラボレーション ルート エンティティ ID:** コラボレーション セッションが参照するビジネス エンティティ ID。
     * **コラボレーション ルート エンティティ名:** コラボレーション セッションが参照するビジネス エンティティの種類名。

     ***詳細オプション:***

      **メタデータの作成 (詳細):** コラボレーション セッション レコードにメタデータを追加します。

      * **OData 型:** 他のキー/値が設定されていて、#Microsoft.Dynamics.CRM.m365_collaborationmetadata と正確に一致する必要がある場合は、このフィールドを指定する必要があります。
      * **キー：** メタデータ属性に関連付けられているキー。
      * **値：** メタデータ属性に関連付けられている値。

      **メタデータの更新 (詳細):** コラボレーション セッション レコードに既存のメタデータを更新します。

      * **OData 型:** 他のキー/値が設定されていて、#Microsoft.Dynamics.CRM.m365_collaborationmetadata と正確に一致する必要がある場合は、このフィールドを指定する必要があります。
      * **キー：** 更新するメタデータ属性に関連付けられているキー。
      * **値：** メタデータ属性に関連付けられている値。

      **メタデータの削除 (詳細):** コラボレーション セッション レコードの既存のメタデータをすべて削除します。

      * **OData 型:** 他のキー/値が設定されていて、#Microsoft.Dynamics.CRM.m365_collaborationmetadata と正確に一致する必要がある場合は、このフィールドを指定する必要があります。
      * **キー：** 削除するメタデータ属性に関連付けられているキー。

  1. コラボレーション マップの関連付け (外部)

      :::image type="content" source="../assets/images/collaboration-control/associate-collab-map.png" alt-text="スクリーンショットは、コラボレーション マップを関連付ける方法を示す例です。":::

     このステップ アクションでは、外部コラボレーション エンティティ (データバースの外部) とコラボレーション セッションのマッピングが作成されます。

     * **コラボレーション ルート ID:** コラボレーション エンティティにマップするコラボレーション セッションの一意の識別子。
     * **コラボレーション マップの外部 ID:** マップする外部コラボレーション リソース ID。
     * **コラボレーション マップ エンティティ名:** マップする外部コラボレーション エンティティの種類名。

     ***詳細オプション:***

     **メタデータ：** コラボレーション マップのメタデータを追加します。
     * **OData 型:** 他のキー/値が設定されていて、#Microsoft.Dynamics.CRM.m365_collaborationmetadata と正確に一致する必要がある場合は、このフィールドを指定する必要があります。
     * **キー：** メタデータ属性に関連付けられているキー。
     * **値：** メタデータ属性に関連付けられている値。

  1. コラボレーション マップの関連付け (内部)

      :::image type="content" source="../assets/images/collaboration-control/associate-collab-map-internal.png" alt-text="スクリーンショットは、コラボレーション マップを内部に関連付ける方法を示す例です。":::

     このステップ アクションでは、コラボレーション セッションとのコラボレーション エンティティ (dataverse テーブル) のマッピングが作成されます。 内部は、内部 Dataverse エンティティ/テーブル間のマッピングのみを作成することを目的としています。

     * **コラボレーション ルート ID:** コラボレーション エンティティにマップするコラボレーション セッションの一意の識別子。
     * **コラボレーション マップ エンティティ ID:** マップする Dataverse コラボレーション エンティティ ID。
     * **コラボレーション マップ エンティティ名:** マップする Dataverse コラボレーション エンティティの種類名。

     ***詳細オプション:***

     **メタデータ (詳細設定)** コラボレーション マップのメタデータを追加します。

     * **OData 型:** 他のキー/値が設定されていて、#Microsoft.Dynamics.CRM.m365_collaborationmetadata と正確に一致する必要がある場合は、このフィールドを指定する必要があります。
     * **キー：** メタデータ属性に関連付けられているキー
     * **値：** メタデータ属性に関連付けられている値

  1. コラボレーション マップを更新する

      :::image type="content" source="../assets/images/collaboration-control/update-collab-map.png" alt-text="スクリーンショットは、コラボレーション マップを更新する方法を示す例です。":::

     このステップ アクションは、既存のコラボレーション マップを更新します。

     * **コラボレーション マップ ID:** コラボレーション マップの一意の識別子を更新します。
     * **コラボレーション マップ エンティティ ID:** マップするコラボレーション エンティティ ID。 外部 ID が指定されている場合は、この値を空にする必要があります
     * **コラボレーション マップ エンティティ名**
     * **コラボレーション マップの外部 ID:** マップする外部コラボレーション リソース ID。 エンティティ ID が指定されている場合は、この値は空にする必要があります。  

     ***詳細オプション:***

     **メタデータの作成:** コラボレーション マップ レコードにさらにメタデータを追加します。

     * **OData 型:** 他のキー/値が設定されていて、#Microsoft.Dynamics.CRM.m365_collaborationmetadata と正確に一致する必要がある場合は、このフィールドを指定する必要があります。
     * **キー：** メタデータ属性に関連付けられているキー。
     * **値：** メタデータ属性に関連付けられている値。

     **メタデータの更新:** コラボレーション マップ レコードに既存のメタデータを更新します。

     * **OData 型:** 他のキー/値が設定されていて、#Microsoft.Dynamics.CRM.m365_collaborationmetadata と正確に一致する必要がある場合は、このフィールドを指定する必要があります。
     * **キー：** 更新するメタデータ属性に関連付けられているキー
     * **値：** メタデータ属性に関連付けられている値

     **メタデータの削除:** コラボレーション マップ レコード上の既存のメタデータをすべて削除します。

     * **OData 型:** 他のキー/値が設定されていて、#Microsoft.Dynamics.CRM.m365_collaborationmetadata と正確に一致する必要がある場合は、このフィールドを指定する必要があります。
     * **キー：** 削除するメタデータ属性に関連付けられているキー。

  1. コラボレーション メタデータを取得する

      :::image type="content" source="../assets/images/collaboration-control/get-collab-metadata.png" alt-text="スクリーンショットは、コラボレーション メタデータを取得する方法を示す例です。":::

     このステップ アクションでは、指定したフィルターに一致するすべてのメタデータが一覧表示されます。

     **フィルター：** メタデータ クエリに適用するフィルター。
     コラボレーション マップ エンティティ ID に関連するすべてのメタデータを取得する例  
     eq 'm365_collaborationmap' と m365_entityid eq 'GUID' をm365_entitynameする

  1. Planner タスクの作成

      :::image type="content" source="../assets/images/collaboration-control/create-planner-task.png" alt-text="スクリーンショットは、プランナー タスクを作成する方法を示す例です。":::

     このステップ アクションは、コラボレーション コントロール Planner タスク仮想テーブルを使用して Graph Planner タスクを作成します。

     * **コラボレーション ルート ID (必須):** コラボレーション セッションの一意識別子
     * **プラン ID (必須):** タスクが属するプラン ID
     * **タイトル (必須):** タスクのタイトル
     * **割り当て：** Task のすべての割り当てを表す json 形式のオブジェクト。 [plannerAssignments リソースの種類を](/graph/api/resources/plannerassignments)参照してください
     * **バケット ID:** タスクが属するバケット ID。
     * **優先 順位：** タスクの優先度。 0 と 10 (包括) の増加値は優先順位が低くなります。

     ***詳細オプション:***

     * **アクティブなチェックリスト項目数** (詳細): 不完全な項目を表す値が false に設定されたチェックリスト アイテムの数。
     * **適用されたカテゴリ:** タスクに適用するすべてのカテゴリを表す json フォーマッタ オブジェクト。 [plannerAppliedCategories リソースの種類を参照してください](/graph/api/resources/plannerappliedcategories)。
     * **担当者の優先度:** リスト ビューでこの型の項目を並べ替えるために使用される文字列値のヒント。 [Planner で注文ヒントを使用する方法を確認する](/graph/api/resources/planner-order-hint-format)
     * **チェックリスト項目数:** タスクに存在するチェックリスト項目の数。
     * **完了者:** タスクを完了したユーザーの ID を表す json 形式のオブジェクト。 [idSet リソースの種類を](/graph/api/resources/identityset)確認する
     * **会話スレッド ID:** タスク上の会話のスレッド ID。 これは、グループに作成された会話スレッド オブジェクトの ID です。
     * **作成者:** タスクを作成したユーザーの ID を表す json 形式のオブジェクト。 [idSet リソースの種類を](/graph/api/resources/identityset)確認する
     * **期限:** タスクの期限の日付と時刻。 Timestamp 型は、ISO 8601 形式を使用して日付と時刻の情報を表し、常に UTC 時間です。 たとえば、2014 年 1 月 1 日の午前 0 時の UTC は 2014-01-01T00:00:00Z です。
     * **注文ヒント:** リスト ビューでこの種類の項目を並べ替えるために使用されるヒント。 この形式は、 [Planner で順序ヒントを使用して](/graph/api/resources/planner-order-hint-format)アウトラインとして定義されます。
     * **達成率:** タスク完了率 (0 ~ 100)
     * **プレビューの種類:** これにより、タスクに表示されるプレビューの種類が設定されます。 可能な値は、自動、noPreview、チェックリスト、説明、リファレンスです。
     * **参照数:** タスクに存在する外部参照の数。
     * **開始日:** タスクが開始される日時。 Timestamp 型は、ISO 8601 形式を使用して日付と時刻の情報を表し、常に UTC 時間です。 たとえば、2014 年 1 月 1 日の午前 0 時の UTC は 2014-01-01T00:00:00Z です。

  1. Planner タスクを取得する

      :::image type="content" source="../assets/images/collaboration-control/get-planner-task.png" alt-text="スクリーンショットは、プランナーの取得タスクを示す例です。":::

     このステップ アクションは、コラボレーション コントロール Planner タスク仮想テーブルを使用して Planner Task データを返します。

     **タスク ID (必須):** タスクの一意識別子

  1. Planner タスクの更新

      :::image type="content" source="../assets/images/collaboration-control/update-planner-task-preview.png" alt-text="スクリーンショットは、Update Planner タスクを示しています。":::

     このステップ アクションは、コラボレーション コントロール Planner タスク仮想テーブルを使用して、Planner タスク レコードを更新します。

     * **タスク ID (必須):** タスクの一意の識別子。
     * **割り当て：** Task のすべての割り当てを表す json 形式のオブジェクト。 plannerAssignments リソースの種類 - Microsoft Graph v1.0 |を参照してくださいMicrosoft Docs。  
     * **バケット ID:** タスクが属するバケット ID。  
     * **Planner タスクの詳細:** タスクに関する追加情報を表します。
     * **期限:** タスクの期限の日付と時刻。 Timestamp 型は、ISO 8601 形式を使用して日付と時刻の情報を表し、常に UTC 時間です。 たとえば、2014 年 1 月 1 日の午前 0 時の UTC は 2014-01-01T00:00:00Z です。
     * **優先 順位：** タスクの優先度。 0 と 10 (包括) の増加値は優先順位が低くなります。  
     * **達成率:** タスクの完了率 (0 ~ 100)。
     * **タイトル：** タスクのタイトル。

     ***詳細オプション:***

     * **適用されたカテゴリ:** タスクに適用するすべてのカテゴリを表す json 形式のオブジェクト。 [plannerAppliedCategories リソースの種類を参照してください](/graph/api/resources/plannerappliedcategories)。
     * **担当者の優先度:** リスト ビューでこの型の項目を並べ替えるために使用される文字列値のヒント。 [Planner で注文ヒントを使用する方法について説明します](/graph/api/resources/planner-order-hint-format)。
     * **会話スレッド ID:** タスク上の会話のスレッド ID。 これは、グループに作成された会話スレッド オブジェクトの ID です。
     * **コラボレーション ルート ID:** コラボレーション セッションの一意識別子。
     * **注文ヒント:** リスト ビューでこの種類の項目を並べ替えるために使用されるヒント。 この形式は、ここでアウトラインとして定義されています。
     * **開始日:** タスクが開始される日時。 Timestamp 型は、ISO 8601 形式を使用して日付と時刻の情報を表し、常に UTC 時間です。 たとえば、2014 年 1 月 1 日の午前 0 時の UTC は 2014-01-01T00:00:00Z です。

**フローシナリオの例**

フローの例を次に示します。

1. Microsoft フォームから応答を取得し、コラボレーション セッションと関連付けられたタスクを作成します。

   :::image type="content" source="../assets/images/collaboration-control/response-submitted.png" alt-text="スクリーンショットは、新しい応答を送信する方法を示す例です。":::

1. コラボレーション セッションが作成されるたびに、詳細をキャプチャして電子メール通知を送信します。

   :::image type="content" source="../assets/images/collaboration-control/colab-session-created-preview.png" alt-text="作成されたコラボレーション セッションを示す例をスクリーンショットに示します。":::

> [!NOTE]
> この方法で複数のフローをトリガーして、コラボレーション セッションの作成の応答からのデータを使用して、さまざまなアクションを実行できます。
