---
title: 仮想テーブル Web API
author: surbhigupta
description: このモジュールでは、コラボレーション コントロール アプリ用の Virtual Tables Web API、Microsoft Teams での仮想テーブルの並べ替え、フィルター処理について説明します。
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: b15c7972dfc0152d458e4ad895ed6d4f7e45cd4c
ms.sourcegitcommit: edfe85e312c73e34aa795922c4b7eb0647528d48
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2022
ms.locfileid: "68243550"
---
# <a name="virtual-tables-web-api"></a>仮想テーブル Web API

Dataverse Web API を使用して仮想テーブルから複数のレコードを取得する場合は、並べ替え、フィルター処理、ページ分割をサポートするために追加のクエリ パラメーターを含めることができます。 これらの機能は、Microsoft Graph APIによって提供されるサポートに依存しているため、コラボレーション コントロールの仮想テーブル全体で一様にサポートされていません。 各仮想テーブルがサポートする内容の詳細については、「仮想テーブル エンティティ リファレンス」を参照してください。

> [!NOTE]
> 現在、コラボレーション コントロールは [パブリック開発者向けプレビュー](~/resources/dev-preview/developer-preview-intro.md)でのみ使用できます。

## <a name="virtual-table-sorting"></a>仮想テーブルの並べ替え

仮想テーブルでは、OData $orderby クエリ パラメーターを使用して、結果セットの並べ替え方法の条件を設定できます。 asc または desc サフィックスを使用して、それぞれ昇順または降順を指定します。 サフィックスが適用されていない場合、既定値は昇順です。  

**サポートされているテーブル**: 各仮想テーブルは、それぞれの Graph リソースと同じ並べ替え機能をサポートします。 並べ替えをサポートする仮想テーブルは次のとおりです。  

* Graph Drive アイテム
* Graph イベント

> [!NOTE]
> 並べ替えは、それぞれの Graph リソースのすべての属性でサポートされているわけではありません。 ユーザーがサポートされていない属性を持つ仮想テーブルで並べ替えようとした場合、この結果セットの既定の順序が設定されます。 これは、並べ替えをサポートしていない列の Dataverse Web API と同じ動作です。

例:

* GET [Organization URI]/api/data/v9.2/m365_graphdriveitems?$filter=m365_collaborationrootid eq '000000-0000-0000-0000-0000-0000000000000'&$orderby=m365_name desc
* GET [Organization URI]/api/data/v9.2/m365_graphevents?$filter=m365_groupid eq '0000000-0000-0000-0000-0000-00000000000'$orderby=m365_subject asc

## <a name="virtual-table-filtering"></a>仮想テーブルのフィルター処理

仮想テーブルでは、OData $filter クエリ パラメーターを使用して、行が返される条件を設定できます。 仮想テーブルは、Dataverse Web API でサポートされているのと同じ OData 演算子を使用してクエリが実行されます。

* **比較演算子**

  |オペレーター|説明|例|
  |----|----|----|
  |eq|等しい|$filter=m365_name eq 'Contoso'|
  |ne|等しくない|$filter=m365_name ne 'Contoso'|
  |gt|大きい|$filter=m365_price gt 50.0|
  |ge|以上または等しい|$filter=m365_price ge 50.0|
  |lt|小さい|$filter=m365_price lt 50.0|
  |le|以下|$filter=m365_price le 50.0|

* **論理演算子**

  |オペレーター|説明|例|
  |----|----|----|
  |and|論理 and |$filter=m365_name eq 'Contoso' と m365_price eq 50.0|
  |or|論理 or |$filter=m365_name ne 'Contoso' または m365_price eq 50.0|
  |not|論理ネゴシエーション |$filter=not contains(m365_name,'Contoso')|

* **グループ化演算子**

  |オペレーター|説明|例|
  |----|----|----|
  |( )|優先順位のグループ化 |$filter=(eq 'Contoso' と m365_price eq 50.0 m365_name) または contains(m365_subject,'Team Sync')|

* **クエリ関数**

  |職務 |例 |
  |----|----|
  |contains|$filter=contains(m365_name,'Contoso')|
  |endswith|$filter=endswith(m365_name,'Contoso')|
  |startswith|$filter=startswith(m365_name,'Contoso')|

**サポートされているテーブル**: 各仮想テーブルは、それぞれの Graph リソースと同じフィルター処理機能をサポートします。 フィルター処理をサポートする仮想テーブルは次のとおりです。

* Graph Booking Appointment
* Graph Drive アイテム
* Graph イベント

> [!Note]
> フィルター処理は、それぞれの Graph リソースのすべての属性ではサポートされていません。 ユーザーがサポートされていない属性を使用して仮想テーブルでフィルター処理しようとすると、このフィルターは無視されます。 これは、フィルター処理をサポートしていない列の Dataverse Web API と同じ動作です。

例:

* GET [Organization URI]/api/data/v9.2/m365_graphbookingappointments?$filter=m365_bookingbusinessid eq 'ContosoBank@Contoso.onmicrosoft.com' と m365_price eq 100.0
* GET [Organization URI]/api/data/v9.2/m365_graphdriveitems?$filter=m365_collaborationrootid eq '0000000-0000-0000-0000-0000-000000000000000' と m365_name eq 'Meeting Notes.docx'
* GET [Organization URI]/api/data/v9.2/m365_graphevents?$filter=m365_groupid eq '0000000-0000-0000-0000-0000-00000-00000000000000000',m365_subject eq 'Monthly Sync'

## <a name="virtual-table-pagination"></a>仮想テーブルの改ページ位置

ページ分割は、大量のレコードセットをフェッチするのに便利なリソースです。 Virtual Table 改ページネーションは、3 つの異なる方法で実現できます。

要求ヘッダーの基本設定値を使用して `odata.maxpagesize` 、ページ サイズを指定できます。 結果セットが複数のページにまたがる場合、応答にはプロパティが `@odata.nextLink` 含まれます。 要求と応答の例は次のとおりです。

# <a name="request"></a>[要求](#tab/request)

```http
  GET [Organization URI]/api/data/v9.2/m365_graphdriveitems 
  Accept: application/json 
  Prefer: odata.maxpagesize=2 
```

# <a name="response"></a>[Response](#tab/response)

```json
{ 

  "@odata.context": "[Organization URI]/api/data/v9.0/$metadata#m365_graphdriveitems", 
  "value": [ 
   { 
      "@odata.etag": "W/\"{FA93AF7C-1F45-4714-85A5-BB95EB86E1E5}\"", 
      "m365_name": "Review.doc", 
      "m365_graphdriveitemid": "f50aae23-6644-3d35-66d7-e3c5a979dad3", 
      …
      },
      {
      "@odata.etag": "W/\"{3938D549-1AEF-46A5-BF3C-38472AD934C2}\"", 
      "m365_name": "Review.doc", 
      "m365_graphdriveitemid": "3d59a7e2-ec83-d0b3-270e-8ad676622027", 
      … 
      } 
      ],
      "@odata.nextLink": "[Organization URI]/api/data/v9.0/m365_graphdriveitems &$skiptoken=%3Ccookie%20pagenumber=%222%22%20pagingcookie=%22UGFnZWQ9VFJVRSZwX1NvcnRCZWhhdmlvcj0xJnBfRmlsZUxlYWZSZWY9dGVzdCZwX0lEPTI5%22%20istracking=%22False%22%20/%3E" 
} 
```

---

現在、次の仮想テーブルで基本設定がサポートされています `odata.maxpagesize` 。

* Graph Booking Appointment
* Graph Calendar イベント
* Graph Drive
* Graph Drive アイテム

URL にオプションを渡 `$top` すことで、返すレコードの数を指定できます。 ページ番号も指定する必要がある場合は、オプションとして XML でエンコードされた文字列としてページング Cookie を `$skiptoken` 渡します。 特定のページ番号をフェッチするには、次の形式でページング Cookie を渡します。

  `<cookie pagenumber=3 />`

# <a name="request"></a>[要求](#tab/request1)

```http
     GET [Organization URL]/api/data/v9.2/m365_graphevents?$top=2&$skiptoken=<cookie pagenumber='3' /> 
```

# <a name="response"></a>[Response](#tab/response1)

```json

{
  "@odata.context": "[Organization URI]/api/data/v9.0/$metadata#m365_graphevents", 
  "value": [
   { 
      "@odata.etag": "W/\"{FA93AF7C-1F45-4714-85A5-BB95EB86E1E5}\"", 
      "m365_graphdeventid": "3d59a7e2-ec83-d0b3-270e-8ad676622027", 
      "m365_subject": "Important meeting", 
      …
    }, 
    {
      "@odata.etag": "W/\"{3938D549-1AEF-46A5-BF3C-38472AD934C2}\"", 
      "m365_graphdeventid": "f50aae23-6644-3d35-66d7-e3c5a979dad3", 
      "m365_subject": "Another important meeting", 
      …
    } 
  ] 
}

```

---

> [!Note]
> 応答にはプロパティは `@nextLink` 含まれません。 ユース ケースで次のページ リンクを返す必要がある場合は、$top URI パラメーターを渡す代わりに、セクション 1 で説明されている odata.maxpagesize 基本設定ヘッダーを使用できます。

現在、次の仮想テーブルでは、特定のページのフェッチがサポートされています。

* Graph Booking Appointment
* Graph Calendar イベント

フェッチ XML は、XML でエンコードされた文字列として渡すことができます。 fetch XML オプションを使用すると、複数のクエリ設定を指定できます。 ページ分割固有のオプションは、ページ (ページ番号) とカウント (ページ サイズ) です。 次の XML は、ページ番号とサイズを指定します。

  `<fetch version="1.0" mapping="logical" returntotalrecordcount="true" page="<Page Number>" count="<Page Size>"></fetch>`

# <a name="request"></a>[要求](#tab/request2)

```http
GET [Organization URL]/api/data/v9.2/m365_graphevents?$fetchXml=<fetch version="1.0" mapping="logical" returntotalrecordcount="true" page="3" count="2"></fetch> 

```

# <a name="response"></a>[Response](#tab/response2)

```json
{ 

    "@odata.context": "[Organization URI]/api/data/v9.0/$metadata#m365_graphdevents", 
    "@Microsoft.Dynamics.CRM.fetchxmlpagingcookie": "<cookie pagenumber=\"3\" pagingcookie=\"\" istracking=\"False\" />", 
    "value": [ 
        { 
            "@odata.etag": "W/\"{FA93AF7C-1F45-4714-85A5-BB95EB86E1E5}\"", 
            "m365_graphdeventid": "3d59a7e2-ec83-d0b3-270e-8ad676622027", 
            "m365_subject": "Important meeting", 
            …
        }, 
        { 
            "@odata.etag": "W/\"{3938D549-1AEF-46A5-BF3C-38472AD934C2}\"", 
            "m365_graphdeventid": "f50aae23-6644-3d35-66d7-e3c5a979dad3", 
            "m365_subject": "Another important meeting", 
            …
        } 
    ] 
} 

```

---

次の仮想テーブルでは、fetchXml オプションの一部として渡される count プロパティがサポートされています。

* Graph Drive
* Graph Drive アイテム

次の仮想テーブルは、fetchXml オプションの一部としてページ プロパティをサポートしています。

* Graph Booking Appointment
* Graph Calendar イベント
