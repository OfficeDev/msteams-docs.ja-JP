---
title: コラボレーション コントロール アプリで外部クライアントのタスクを構成する
author: surbhigupta
description: このモジュールでは、Microsoft Teams のコラボレーション コントロール アプリで外部クライアントのタスクを構成する方法について説明します。
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: 7d458cc97429772695958606835edd4ef953b5db
ms.sourcegitcommit: edfe85e312c73e34aa795922c4b7eb0647528d48
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2022
ms.locfileid: "68243165"
---
# <a name="configure-tasks-for-external-clients"></a>外部クライアントのタスクを構成する

組織の一部ではないユーザーや、顧客にタスクを割り当てるなど、アプリケーションにアクセスできないユーザーに割り当てることができる外部タスク。

有効にするには、必要な MDA フォームのサブグリッド コンポーネントにアタッチされている Tasks PCF コントロールの各インスタンスに XML 文字列を渡す追加の手順が必要です。 XML 文字列はパラメーター化されたクエリであり、コントロールは顧客情報を含むテーブルから必要なデータを抽出できます。

> [!NOTE]
> 現在、コラボレーション コントロールは [パブリック開発者向けプレビュー](~/resources/dev-preview/developer-preview-intro.md)でのみ使用できます。

外部タスクを作成するには、次の手順に従います。

1. Customer などの新しいカスタム エンティティを作成するか、連絡先などの既存の顧客エンティティを再利用します。

1. 次の情報を保持する新しいフィールドを作成します。
    1. 名前
    1. メール
    1. 親 (検査などの親テーブルへの参照)
    > [!NOTE]
    > 上記で作成した顧客エンティティは、タスク コントロールが外部タスクを割り当てるときに顧客情報をプルします。 親フィールドは、顧客エンティティが検査レコードにリンクされていることを確認します。

1. フェッチ XML ファイルを生成して、PCF コントロールが適切な顧客情報をプルできるようにします。

    **XML スキーマを構成する**

    タスク構成 Fetch XML のスキーマ定義を次に示します。 Fetch XML は、次の要件を満たすように設計する必要があります。

    * クエリ結果は、各ユーザー オブジェクトに対して次のプロパティを返す必要があります。
      * ID
      * Displayname
      * 電子メールは、必要に応じてエイリアスを使用します。
    * クエリには、呼び出し元が結果の数を制限できるように、 **@top** パラメーターが含まれている必要があります。
    * クエリには、必要 **に応** じて、関連レコードだけで結果をフィルター処理するパラメーター@rootEntityId必要があります。
    * クエリには **、** 名前による結果のフィルター処理を許可するパラメーター@useName必要があります
    * クエリには、選択したユーザーのみをフェッチできるように、 **@useIdentifier** パラメーターが必要です。

    **構成 XML スキーマと例**

    XML スキーマの構成では、顧客テーブルからデータがプルされます。 ノードを調整して、独自の `<fetch/>` クエリを指定して、他のカスタム テーブルのユーザーを表示できます。

    > [!NOTE]
    > XML 内の上記のエンティティと属性名と順序属性は **、PublisherPrefix_TableColumn** 形式です。

    ```xml
    
    <custom-tasks> 
    <custom-task id="external" name="External" for="guest"> 
    <fetch top="@top"> 
    <entity name="[Name of table, e.g. Crb2891_customer]"> 
    <attribute name="[Name of ID column, e.g. Crb2891_customerid]" alias="id" /> 
    <attribute name="[Name of primary name column, e.g. Crb2891_name]" alias="displayname" /> 
    <attribute name="[Name of email column, e.g. Crb2891_email]" alias="email" /> 
    <order attribute ="[Name of primary name column, e.g. Crb2891_name]" descending="false" /> 
    <filter type="and"> 
    <condition attribute="[Name of parent lookup column, e.g. Crb2891_parent]" operator="eq" value="@rootEntityId" /> 
    <condition attribute="[Name of primary name column, e.g. Crb2891_name]" operator="like" value="@userName" /> 
    <condition attribute="[Name of email column, e.g. Crb2891_email]" operator="like" value="@userIdentifier" /> 
    </filter> 
    </link-entity> 
    </entity> 
    </fetch> 
    </custom-task> 
    </custom-tasks> 
    
    ```

1. タスク コントロールをクラシック フォーム デザイナー内のサブグリッドにバインドします。 **[保存] を** 選択し、[**クラシックに切り替える**] を選択します。

1. [ **タスク** ] タブが見つかるまで、クラシック フォーム デザイナー内を移動します。サブグリッドをダブルクリックして、そのプロパティ ダイアログを開きます。

    :::image type="content" source="~/assets/images/collaboration-control/subgrid-property.png" alt-text="タスク プロパティ ダイアログを示すスクリーンショット。":::

1. プロパティ ダイアログで、次の図に示すようにプロパティを設定します。

    :::image type="content" source="~/assets/images/collaboration-control/tasks-property.png" alt-text="Sceenshot は、Tasks プロパティの設定でプロパティを設定することを示しています。":::

1. [コントロール] タブに移動し、[スクリーンショット] を選択 :::image type="icon" source="~/assets/images/collaboration-control/edit-icon.png" alt-text="してタスクを編集する方法を示します。"::: をクリックして、上記で生成された Fetch XML を追加します。

1. Fetch XML を貼り付ける

    :::image type="content" source="~/assets/images/collaboration-control/set-fetchproperties.png" alt-text="Fetch XML を貼り付ける方法を示すスクリーンショット。":::

    :::image type="content" source="~/assets/images/collaboration-control/custom-tasksproperty.png" alt-text="スクリーンショットは、カスタム プロパティ設定を構成する方法を示しています。":::

1. [プロパティの構成] の [カスタム タスク] ウィンドウと [プロパティの設定] ウィンドウで **[OK] を選択します** 。

1. 保存して発行します。
