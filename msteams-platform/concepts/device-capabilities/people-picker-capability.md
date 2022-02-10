---
title: ユーザー ピッカーを統合する
author: Rajeshwari-v
description: JavaScript クライアント SDK Teamsを使用して People Picker コントロールを統合する方法
keywords: ユーザー選択コントロール
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: surbhigupta
ms.openlocfilehash: 7a7a229bdeab7d83f71f8dbe3b24da8b44b3db32
ms.sourcegitcommit: 90587b1ec04bf20d716ed6feb8ccca4313e87f8c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2022
ms.locfileid: "62518143"
---
# <a name="integrate-people-picker"></a>ユーザー ピッカーを統合する  

[ユーザー選択] は、ユーザーを検索して選択するコントロールです。 これは、プラットフォームで使用できるネイティブTeamsです。 ネイティブのユーザー選択Teamsコントロールを Web アプリと統合できます。 単一または複数の選択、および構成 (チャット、チャネル、組織全体での検索の制限など) を選択できます。

Web アプリ内[Microsoft Teams統合する API](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) を提供する JavaScript クライアント SDK `selectPeople` を使用できます。 

## <a name="advantages-of-integrating-the-native-people-picker"></a>ネイティブの People Picker を統合する利点 

* ユーザー選択コントロールは、タスク モジュールTeams、チャネル、会議タブ、個人用アプリなど、すべてのユーザー のサーフェスで機能します。
* このコントロールを使用すると、チャット、チャネル、または組織全体のユーザーを検索して選択できます。
* ユーザー選択ウィンドウは、タスクの割り当て、タグ付け、ユーザーへの通知に関するシナリオに役立ちます。 
* この簡単に利用できるコントロールは、Web アプリで使用できます。 このようなコントロールを独自に構築する労力と時間を大幅に節約できます。

ユーザー選択コントロールをアプリ`selectPeople`に統合するには、API を呼び出Teamsがあります。 効果的な統合を行う場合は、API を呼び出 [すコード スニペット](#code-snippet) について理解している必要があります。 Web アプリのエラーを処理するには [、API](#error-handling) 応答エラーについて理解することが重要です。

> [!NOTE] 
> 現在、Microsoft Teamsユーザー選択のサポートはモバイル クライアントでのみ利用できます。

## <a name="selectpeople-api"></a>`selectPeople` API 

`selectPeople`API を使用すると、web アプリTeamsネイティブなアプリ`People Picker input control`を追加できます。  
API の説明は次のとおりです。

| API      | [説明]  |
| --- | --- |
|**selectPeople**|ユーザー選択ツールを起動し、ユーザーがリストから 1 人または複数のユーザーを検索して選択できます。<br/><br/>この API は、選択したユーザーの ID、名前、電子メール アドレスを呼び出し元の Web アプリに返します。<br/><br/>個人用アプリの場合、コントロールは組織全体を検索します。 アプリがチャットまたはチャネルに追加された場合、シナリオに応じて検索コンテキストが構成されます。 検索は、そのチャット、チャネルのメンバー内で制限されている、または組織全体で利用できます。|

API `selectPeople` には、次の入力構成が付属しています。

|構成パラメーター|種類|説明| 既定値|
|-----|------|--------------|------|
|`title`| String| これはオプションのパラメーターです。 ユーザー選択コントロールのタイトルを設定します。 | ユーザーを選択する|
|`setSelected`|String| これはオプションのパラメーターです。 事前に選択Microsoft Azure Active Directory (Azure AD) のユーザーの ID を渡す必要があります。 このパラメーターは、ユーザー選択コントロールの起動中にユーザーを事前に選択します。 1 つの選択の場合、最初の有効なユーザーだけが、残りのユーザーを無視して事前設定されます。 |Null| 
|`openOrgWideSearchInChatOrChannel`|Boolean | これはオプションのパラメーターです。 true に設定すると、アプリがチャットやチャネルに追加された場合でも、組織全体のスコープでユーザー選択を起動します。 |False|
|`singleSelect`|Boolean|これはオプションのパラメーターです。 true に設定すると、選択を 1 人のユーザーにのみ制限するユーザー選択を起動します。 |False|

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

|エラー コード |  エラー名     | 条件|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | API は現在のプラットフォームではサポートされていません。|
| **500** | INTERNAL_ERROR | ユーザー選択の起動中に内部エラーが発生しました。|
| **4000** | INVALID_ARGUMENTS | API は、間違った引数または不十分な必須引数を使用して呼び出されます。|
| **8000** | USER_ABORT |ユーザーが操作を取り消しました。|
| **9000** | OLD_PLATFORM | ユーザーは、API の実装が存在しない古いプラットフォーム ビルドに存在します。  ビルドをアップグレードすると、問題が解決します。|

## <a name="see-also"></a>関連項目

* [Teams でメディア機能を統合する](mobile-camera-image-permissions.md)
* [QR コードまたはバーコード スキャナー機能をアプリに統合Teams](qr-barcode-scanner-capability.md)
* [Teams で位置情報機能を統合する](location-capability.md)
