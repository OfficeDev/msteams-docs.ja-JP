---
title: ユーザー ピッカーを統合する
author: Rajeshwari-v
description: JavaScript クライアント SDK Teamsを使用して People Picker コントロールを統合する方法
keywords: ユーザー選択コントロール
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: surbhigupta
ms.openlocfilehash: 5f686b247397c89a5a1ab8fe80ac9e97017ea051
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2021
ms.locfileid: "59156595"
---
# <a name="integrate-people-picker"></a>ユーザー ピッカーを統合する  

[ユーザー選択] は、ユーザーを検索して選択するコントロールです。 これは、プラットフォームで使用できるネイティブTeamsです。 ネイティブのユーザー選択Teamsコントロールを Web アプリと統合できます。 単一または複数の選択、および構成 (チャット、チャネル、組織全体での検索の制限など) を選択できます。

JavaScript クライアント SDK [Microsoft Teamsを](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)使用して、Web アプリ内に `selectPeople` People Picker を統合する API を提供します。 

## <a name="advantages-of-integrating-the-native-people-picker"></a>ネイティブの People Picker を統合する利点 

* ユーザー選択コントロールは、タスク モジュールTeams、チャネル、会議タブ、個人用アプリなど、すべてのユーザー のサーフェスで機能します。
* このコントロールを使用すると、チャット、チャネル、または組織全体のユーザーを検索して選択できます。
* ユーザー選択ウィンドウは、タスクの割り当て、タグ付け、ユーザーへの通知に関するシナリオに役立ちます。 
* この簡単に利用できるコントロールは、Web アプリで使用できます。 このようなコントロールを独自に構築する労力と時間を大幅に節約できます。

ユーザー選択コントロールを `selectPeople` アプリに統合するには、API を呼び出Teamsがあります。 効果的な統合を行う場合は、API を呼び出 [すコード スニペット](#code-snippet) について理解している必要があります。 Web アプリのエラーを処理するには [、API](#error-handling) 応答エラーについて理解することが重要です。

> [!NOTE] 
> 現在、Microsoft Teamsユーザー選択のサポートはモバイル クライアントでのみ利用できます。

## <a name="selectpeople-api"></a>`selectPeople` API 

`selectPeople`API を使用すると、web アプリTeamsネイティブ `People Picker input control` なアプリを追加できます。  
API の説明は次のとおりです。

| API      | 説明  |
| --- | --- |
|**selectPeople**|ユーザー選択ツールを起動し、ユーザーがリストから 1 人または複数のユーザーを検索して選択できます。<br/><br/>この API は、選択したユーザーの ID、名前、電子メール アドレスを呼び出し元の Web アプリに返します。<br/><br/>個人用アプリの場合、コントロールは組織全体を検索します。 アプリがチャットまたはチャネルに追加された場合、シナリオに応じて検索コンテキストが構成されます。 検索は、そのチャット、チャネルのメンバー内で制限されている、または組織全体で利用できます。|

`selectPeople`API には、次の入力構成が付属しています。

|構成パラメーター|型|説明| 既定値|
|-----|------|--------------|------|
|`title`| String| これはオプションのパラメーターです。 ユーザー選択コントロールのタイトルを設定します。 | ユーザーを選択する|
|`setSelected`|String| これはオプションのパラメーターです。 事前に選択するユーザーの AAD の ID を渡す必要があります。 このパラメーターは、ユーザー選択コントロールの起動中にユーザーを事前に選択します。 1 つの選択の場合、最初の有効なユーザーだけが、残りのユーザーを無視して事前設定されます。 |Null| 
|`openOrgWideSearchInChatOrChannel`|ブール値 | これはオプションのパラメーターです。 true に設定すると、アプリがチャットやチャネルに追加された場合でも、組織全体のスコープでユーザー選択を起動します。 |False|
|`singleSelect`|ブール値|これはオプションのパラメーターです。 true に設定すると、選択を 1 人のユーザーにのみ制限するユーザー選択を起動します。 |False|

次の図は、サンプル Web アプリでの People Picker のエクスペリエンスを示しています。

![ユーザー選択の Web アプリ エクスペリエンス](../../assets/images/tabs/people-picker-control-capability.png)

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