---
title: ユーザー選択機能の統合
author: Rajeshwari-v
description: JavaScript クライアント SDK Teamsを使用してユーザー選択機能を統合する方法
keywords: ユーザー選択コントロール
ms.topic: conceptual
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: 8399eeb1a088e4b60c466d51c223b9405ebf1711
ms.sourcegitcommit: 059d22c436ee9b07a61561ff71e03e1c23ff40b8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2021
ms.locfileid: "53211637"
---
# <a name="integrate-people-picker-capability"></a>ユーザー選択機能の統合 

[ユーザー選択] は、ユーザーを検索して選択するコントロールです。 これは、プラットフォームで使用できるネイティブTeamsです。 ネイティブのユーザー選択Teamsコントロールを Web アプリと統合できます。 単一または複数の選択、および構成 (チャット、チャネル、組織全体での検索の制限など) を選択できます。

Web アプリ内Microsoft Teamsユーザー選択機能を統合する API を提供する[JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)クライアント SDK を `selectPeople` 使用できます。 

## <a name="advantages-of-integrating-people-picker-capability"></a>ユーザー選択機能を統合する利点

* People Picker コントロールは、タスク モジュール、Teams、チャネル、会議タブ、個人用アプリなど、すべてのユーザー 選択サーフェスで機能します。
* このコントロールを使用すると、チャット、チャネル、または組織全体のユーザーを検索して選択できます。
*  ユーザー選択機能は、タスクの割り当て、タグ付け、ユーザーへの通知に関するシナリオに役立ちます。 
* この簡単に利用できるコントロールは、Web アプリで使用できます。 このようなコントロールを独自に構築する労力と時間を大幅に節約できます。

ユーザー選択コントロールを `selectPeople` アプリに統合するには、API を呼び出Teamsがあります。 効果的な統合を行う場合は、API を呼び出 [すコード スニペット](#code-snippet) について理解している必要があります。 Web アプリのエラーを処理するには [、API](#error-handling) 応答エラーについて理解することが重要です。

> [!NOTE] 
> 現在、Microsoft Teamsユーザー選択機能のサポートはモバイル クライアントでのみ利用できます。

## <a name="selectpeople-api"></a>`selectPeople` API 

`selectPeople`API を使用すると、web アプリTeamsネイティブ `People Picker input control` なアプリを追加できます。  
API の説明は次のとおりです。

| API      | 説明  |
| --- | --- |
|**selectPeople**|ユーザー選択ツールを起動し、ユーザーがリストから 1 人または複数のユーザーを検索して選択できます。<br/><br/>この API は、選択したユーザーの ID、名前、電子メール アドレスを呼び出し元の Web アプリに返します。<br/><br/>個人用アプリの場合、コントロールは組織全体を検索します。 アプリがチャットまたはチャネルに追加された場合、シナリオに応じて検索コンテキストが構成されます。 検索は、そのチャット、チャネルのメンバー内で制限されている、または組織全体で利用できます。|

`selectPeople`API には、次の入力構成が付属しています。

|構成パラメーター|種類|説明| 既定値|
|-----|------|--------------|------|
|`title`| String| これはオプションのパラメーターです。 ユーザー選択コントロールのタイトルを設定します。 | ユーザーを選択する|
|`setSelected`|String| これはオプションのパラメーターです。 事前に選択するユーザーの AAD の ID を渡す必要があります。 このパラメーターは、ユーザー選択コントロールの起動中にユーザーを事前に選択します。 1 つの選択の場合、最初の有効なユーザーだけが、残りのユーザーを無視して事前設定されます。 |Null| 
|`openOrgWideSearchInChatOrChannel`|Boolean | これはオプションのパラメーターです。 true に設定すると、アプリがチャットやチャネルに追加された場合でも、組織全体のスコープでユーザー選択を起動します。 |False|
|`singleSelect`|Boolean|これはオプションのパラメーターです。 true に設定すると、選択を 1 人のユーザーにのみ制限するユーザー選択を起動します。 |False|

次の図は、サンプル Web アプリでのユーザー選択機能のエクスペリエンスを示しています。

![ユーザー選択機能の Web アプリ エクスペリエンス](../../assets/images/tabs/people-picker-control-capability.png)

### <a name="code-snippet"></a>コード スニペット

**通話 `selectPeople` リスト** からユーザーを選択する API:

```javascript
 microsoftTeams.people.selectPeople((error: microsoftTeams.SdkError, people: microsoftTeams.people.PeoplePickerResult[]) => 
 {
    if (error) 
    {
        if (error.message) 
           {
             alert(" ErrorCode: " + error.errorCode + error.message);
           }
            else 
            {
              alert(" ErrorCode: " + error.errorCode);
            }
      }
    if (people)
     {
            output(" People length: " + people.length + " " + JSON.stringify(people));
      }
  });
```

## <a name="error-handling"></a>エラー処理

Web アプリでエラーを適切に処理する必要があります。 次の表に、エラー コードとエラーが生成される条件を示します。 

|エラー コード |  エラー名     | Condition|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | API は現在のプラットフォームではサポートされていません。|
| **500** | INTERNAL_ERROR | ユーザー選択の起動中に内部エラーが発生しました。|
| **4000** | INVALID_ARGUMENTS | API は、間違った引数または不十分な必須引数を使用して呼び出されます。|
| **8000** | USER_ABORT |ユーザーが操作を取り消しました。|
| **9000** | OLD_PLATFORM | ユーザーは、API の実装が存在しない古いプラットフォーム ビルドに存在します。  ビルドをアップグレードすると、問題が解決します。|

## <a name="see-also"></a>関連項目

* [メディア機能を統合Teams](mobile-camera-image-permissions.md)
* [QR コードまたはバーコード スキャナー機能をアプリに統合Teams](qr-barcode-scanner-capability.md)
* [場所の機能を統合Teams](location-capability.md)
