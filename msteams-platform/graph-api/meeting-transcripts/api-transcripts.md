---
title: Graph API を使用してトランスクリプトをフェッチする
description: 会議のトランスクリプトをフェッチするための API について説明します
ms.localizationpriority: high
ms.topic: concept
ms.openlocfilehash: c3882134a9954cff3f2cd4aa038902540a6af250
ms.sourcegitcommit: 990a36fb774e614146444d4adaa2c9bcdb835998
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2022
ms.locfileid: "67232407"
---
# <a name="use-graph-apis-to-fetch-transcript"></a>Graph API を使用してトランスクリプトをフェッチする

Graph REST API を使用して、特定の会議のトランスクリプトを取得します。 アプリは、会議の開催者のユーザー ID と会議 ID に基づいてトランスクリプトをフェッチします。

トランスクリプトのフェッチには、次の API が使用されます。

- [List callTranscripts](#list-calltranscripts)
- [Get callTranscript](#get-calltranscript)
- [Get callTranscript content](#get-calltranscript-content)

### <a name="list-calltranscripts"></a>List callTranscripts

この API は、ユーザー ID と会議 ID に基づいてすべての `callTranscript` オブジェクトの一覧を取得するために使用されます。 会議のトランスクリプトのメタデータを返します。これには、トランスクリプト ID とそのトランスクリプトの作成日時が含まれます。

**HTTP 要求**

```http
GET /me/onlineMeetings('{meetingId}')/transcripts
GET /users('{userId}')/onlineMeetings('{meetingId}')/transcripts
```

**オプションのクエリ パラメーター**

このメソッドは、応答をカスタマイズするための `$skipToken` および `$top` [OData クエリ パラメーター](/graph/query-parameters)をサポートします。

**サポートされているクエリ パターン**

| パターン                | サポート | 構文                                 | メモ |
| ---------------------- | ------- | -------------------------------------- | ----- |
| サーバー側の改ページ位置の自動修正 |     ✓     | `@odata.nextLink`                      | 結果セットが複数のページにまたがる場合は、応答で継続トークンを取得します。 |
| ページの制限             |     ✓     | `/transcripts?$top=20` | ページ サイズ 20 のトランスクリプトを取得します。 既定のページ制限は 10 です。 ページの上限は 100 です。 |

**要求ヘッダー**

| ヘッダー       | 値 |
|:---------------|:--------|
| Authorization  | ベアラー {token}。必須。  |

**要求本文**

このメソッドには、要求本文を指定しません。

**応答**

成功した場合、このメソッドは `200 OK` 応答コードと、応答本文で `callTranscript` オブジェクトのコレクションを返します。

<br>
<details>
<summary><b>例: callTranscript の一覧</b></summary>
<br>
<b>要求</b>
<br>

```http
GET https://graph.microsoft.com/beta/users/ba321e0d-79ee-478d-8e28-85a19507f456/onlineMeetings/MSo1N2Y5ZGFjYy03MWJmLTQ3NDMtYjQxMy01M2EdFGkdRWHJlQ/transcripts
```

<br>
<b>応答</b>
<br>

> [!NOTE]
> ここに示す応答オブジェクトは、読みやすさのために短縮されている可能性があります。

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#users('ba321e0d-79ee-478d-8e28-85a19507f456')/onlineMeetings('MSo1N2Y5ZGFjYy03MWJmLTQ3NDMtYjQxMy01M2EdFGkdRWHJlQ')/transcripts",
    "@odata.count": 3,
    "@odata.nextLink": "https://graph.microsoft.com/beta/users('ba321e0d-79ee-478d-8e28-85a19507f456')/onlineMeetings('MSo1N2Y5ZGFjYy03MWJmLTQ3NDMtYjQxMy01M2EdFGkdRWHJlQ')/transcripts?$skiptoken=MSMjMCMjMjAyMS0wOS0xNlQxMzo1OToyNy4xMjEwMzgzWg%3d%3d",
    "value": [
        {
            "id": "MSMjMCMjZDAwYWU3NjUtNmM2Yi00NjQxLTgwMWQtMTkzMmFmMjEzNzdh",
            "createdDateTime": "2021-09-17T06:09:24.8968037Z"
        },
        {
            "id": "MSMjMCMjMzAxNjNhYTctNWRmZi00MjM3LTg5MGQtNWJhYWZjZTZhNWYw",
            "createdDateTime": "2021-09-16T18:58:58.6760692Z"
        },
        {
            "id": "MSMjMCMjNzU3ODc2ZDYtOTcwMi00MDhkLWFkNDItOTE2ZDNmZjkwZGY4",
            "createdDateTime": "2021-09-16T18:56:00.9038309Z"
        }        
    ]
}
```

</details>

### <a name="get-calltranscript"></a>Get callTranscript

アプリは、`List callTranscripts` API の応答として受信したトランスクリプト ID の一覧を解析して、必要なトランスクリプト ID を取得します。 この API は、ユーザー ID、会議 ID、およびトランスクリプト ID に基づいて 1 つのトランスクリプト メタデータを取得するために使用されます。

**HTTP 要求**

```http
GET me/onlineMeetings('{meetingId}')/transcripts('{transcriptId}')
GET users('{userId}')/onlineMeetings('{meetingId}')/transcripts('{transcriptId}')
```

**要求ヘッダー**

| ヘッダー       | 値 |
|:---------------|:--------|
| Authorization  | ベアラー {token}。必須。  |

**要求本文**

このメソッドには、要求本文を指定しません。

**応答**

成功した場合、このメソッドは `200 OK` 応答コードと、応答本文で`callTranscript` オブジェクトを返します。

<br>
<details>
<summary><b>例: callTranscript を取得する</b></summary>
<br>
<b>要求</b>
<br>

```http
GET https://graph.microsoft.com/beta/users/ba321e0d-79ee-478d-8e28-85a19507f456/onlineMeetings/MSo1N2Y5ZGFjYy03MWJmLTQ3NDMtYjQxMy01M2EdFGkdRWHJlQ/transcripts/MSMjMCMjNzU3ODc2ZDYtOTcwMi00MDhkLWFkNDItOTE2ZDNmZjkwZGY4
```

<br>
<b>Response</b>
<br>

> [!NOTE]
> ここに示す応答オブジェクトは、読みやすさのために短縮されている可能性があります。

```http
HTTP/1.1 200 OK
Content-type: application/json

{
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#users('ba321e0d-79ee-478d-8e28-85a19507f456')/onlineMeetings('MSo1N2Y5ZGFjYy03MWJmLTQ3NDMtYjQxMy01M2EdFGkdRWHJlQ')/transcripts/$entity",
    "id": "MSMjMCMjNzU3ODc2ZDYtOTcwMi00MDhkLWFkNDItOTE2ZDNmZjkwZGY4",
    "createdDateTime": "2021-09-17T06:09:24.8968037Z"
}
```

</details>

### <a name="get-calltranscript-content"></a>Get callTranscript content

この API は、`Get callTranscript` API の応答で取得された、選択したトランスクリプト ID のトランスクリプトを取得するために使用されます。 トランスクリプトの内容を返します。

**HTTP 要求**

```http
GET me/onlineMeetings('{meetingId}')/transcripts('{transcriptId}')/content
GET users('{userId}')/onlineMeetings('{meetingId}')/transcripts('{transcriptId}')/content
```

**オプションのクエリ パラメーター**

このメソッドは、応答のカスタマイズを可能にする `$format` [OData クエリ パラメーター](/graph/query-parameters) をサポートします。

サポートされている形式の種類は、vtt に対する `text/vtt`、または docx に対する `application/vnd.openxmlformats-officedocument.wordprocessingml.document` 形式です。

**要求ヘッダー**

| ヘッダー       | 値 |
|:---------------|:--------|
| Authorization  | ベアラー {token}。必須。  |
| 承諾  | text/vtt または application/vnd.openxmlformats-officedocument.wordprocessingml.document. オプション。  |

**要求本文**

このメソッドには、要求本文を指定しません。

**Response**

成功した場合、このメソッドは `200 OK` 応答コードと、応答本文で callTranscript オブジェクトの特定のバイトを返します。 `content-type` ヘッダーでは、トランスクリプト コンテンツの種類を指定します。

**例**
<br>
<details>
<summary><b>例: callTranscript コンテンツを取得する</b></summary>
<br>
<b>要求</b>
<br>

```http
GET https://graph.microsoft.com/beta/users/ba321e0d-79ee-478d-8e28-85a19507f456/onlineMeetings/MSo1N2Y5ZGFjYy03MWJmLTQ3NDMtYjQxMy01M2EdFGkdRWHJlQ/transcripts/MSMjMCMjNzU3ODc2ZDYtOTcwMi00MDhkLWFkNDItOTE2ZDNmZjkwZGY4/content
```

<br>
<b>Response</b>
<br>

応答には、本文内のトランスクリプトのバイトが含まれます。 `content-type` ヘッダーでは、トランスクリプト コンテンツの種類を指定します。

> [!NOTE]
> ここに示す応答オブジェクトは、読みやすさのために短縮されている可能性があります。

```http
HTTP/1.1 200 OK
Content-type: text/vtt

WEBVTT
    
0:0:0.0 --> 0:0:5.320
<v User Name>This is a transcript test.</v>
```

</details>
<br>
<details>
<summary><b>例: $format クエリ パラメーターを指定して callTranscript コンテンツを取得する</b></summary>
<br>
<b>要求</b>
<br>

```http
GET https://graph.microsoft.com/beta/users/ba321e0d-79ee-478d-8e28-85a19507f456/onlineMeetings/MSo1N2Y5ZGFjYy03MWJmLTQ3NDMtYjQxMy01M2EdFGkdRWHJlQ/transcripts/MSMjMCMjNzU3ODc2ZDYtOTcwMi00MDhkLWFkNDItOTE2ZDNmZjkwZGY4/content?$format=text/vtt
 ```

<br>
<b>Response</b>
<br>

応答には、本文内のトランスクリプトのバイトが含まれます。 `content-type` ヘッダーでは、トランスクリプト コンテンツの種類を指定します。

> [!NOTE]
> ここに示す応答オブジェクトは、読みやすさのために短縮されている可能性があります。

```http
HTTP/1.1 200 OK
Content-type: text/vtt
    
WEBVTT
    
0:0:0.0 --> 0:0:5.320
<v User Name>This is a transcript test.</v>
```

</details>
<br>
<details>
<summary><b>例: Accept ヘッダーを指定して callTranscript コンテンツを取得する</b></summary>
<br>
<b>要求</b>
<br>

```http
GET https://graph.microsoft.com/beta/users/ba321e0d-79ee-478d-8e28-85a19507f456/onlineMeetings/MSo1N2Y5ZGFjYy03MWJmLTQ3NDMtYjQxMy01M2EdFGkdRWHJlQ/transcripts/MSMjMCMjNzU3ODc2ZDYtOTcwMi00MDhkLWFkNDItOTE2ZDNmZjkwZGY4/content
Accept: application/vnd.openxmlformats-officedocument.wordprocessingml.document
```

<br>
<b>Response</b>
<br>

応答には、本文内のトランスクリプトのバイトが含まれます。 `content-Type` ヘッダーでは、トランスクリプト コンテンツの種類を指定します。

> [!NOTE]
> ここに示す応答オブジェクトは、読みやすさのために短縮されている可能性があります。

```http
HTTP/1.1 200 OK
Content-type: application/vnd.openxmlformats-officedocument.wordprocessingml.document
    
0:0:0.0 --> 0:0:5.320
User Name
This is a transcript test.
```

</details>
<br>
<details>
<summary><b>例: accept ヘッダーよりも優先される $format を使って callTranscript コンテンツを取得する</b></summary>
<br>
<b>要求</b>
<br>

```http
GET https://graph.microsoft.com/beta/users/ba321e0d-79ee-478d-8e28-85a19507f456/onlineMeetings/MSo1N2Y5ZGFjYy03MWJmLTQ3NDMtYjQxMy01M2EdFGkdRWHJlQ/transcripts/MSMjMCMjNzU3ODc2ZDYtOTcwMi00MDhkLWFkNDItOTE2ZDNmZjkwZGY4/content?$format=text/vtt
Accept: application/vnd.openxmlformats-officedocument.wordprocessingml.document
```

<br>
<b>Response</b>
<br>

応答には、本文内のトランスクリプトのバイトが含まれます。 `content-Type` ヘッダーでは、トランスクリプト コンテンツの種類を指定します。

> [!NOTE]
> ここに示す応答オブジェクトは、読みやすさのために短縮されている可能性があります。

```http
HTTP/1.1 200 OK
Content-type: text/vtt
    
WEBVTT
   
0:0:0.0 --> 0:0:5.320
<v User Name>This is a transcript test.</v>
```

</details>

