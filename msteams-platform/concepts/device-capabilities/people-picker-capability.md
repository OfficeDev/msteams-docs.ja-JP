---
title: ユーザー ピッカーを統合する
description: この記事では、Teams JavaScript クライアント SDK を使用してユーザー ピッカー コントロールを統合する方法と、ユーザーピッカーを使用する利点について説明します。
ms.topic: conceptual
ms.localizationpriority: high
ms.author: surbhigupta
ms.openlocfilehash: 5a45f2c3a7d098bfe95b55620fb5909fb33e3472
ms.sourcegitcommit: 79d525c0be309200e930cdd942bc2c753d0b718c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/19/2022
ms.locfileid: "66842004"
---
# <a name="integrate-people-picker"></a>ユーザー ピッカーを統合する

ユーザー ピッカーは、ユーザーがユーザーを検索して選択できるようにする Teams の入力コントロールです。 入力コントロールユーザー ピッカー を Web アプリに統合できます。これにより、エンド ユーザーは、Teams 内のチャット、チャネル、組織全体のユーザーの検索や選択などのさまざまな機能を実行できます。 ユーザー ピッカー コントロールは、Web、デスクトップ、モバイルなど、すべての Teams クライアントで使用できます。

[Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) を使用できます。これにより、`selectPeople` API を使用して、ユーザー ピッカー入力コントロールを Web アプリに統合できます。

## <a name="advantages-of-using-people-picker"></a>ユーザー ピッカーを使用する利点

* タスク モジュール、チャット、チャネル、会議タブ、個人用アプリなど、Teams のすべての機能で動作します。
* ユーザーが Teams 内のチャット、チャネル、または組織全体のユーザーを検索して選択できるようにします。
* タスクの割り当て、タグ付け、ユーザーへの通知に関連するシナリオで役立ちます。
* 同様のコントロールを構築する場合と比較して、大幅な時間と労力を節約できます。

Teams アプリでユーザー ピッカー入力コントロールを統合するには、[`selectPeople`](#selectpeople-api) API を使用します。 API を統合して呼び出すには、付随する [code スニペット](#code-snippet) をよく理解している必要があります。 また、[API 応答エラー](#error-handling) についての知識も必要です。

## <a name="selectpeople-api"></a>`selectPeople` API

`selectPeople` API を使用すると、Teams ユーザー ピッカー入力コントロールを Web アプリに追加したり、次の操作を行うこともできます。

* ユーザーがリストから 1 人以上のユーザーを検索して選択できるようにします。
* 選択したユーザーの ID、名前、電子メール アドレスを Web アプリに返します。

個人用アプリの場合、コントロールは Teams 内で組織全体の名前または電子メール ID を検索します。 アプリがチャットまたはチャネルに追加された場合、検索コンテキストはシナリオに基づいて構成されます。 検索は、そのチャットまたはチャネルのメンバー内で制限されます。

`selectPeople` API には、次の入力構成が付属しています。

|構成パラメーター|型|説明| 既定値|
|-----|------|--------------|------|
|`title`|String| これは省略可能なパラメーターであり、ユーザー ピッカー コントロールのタイトルを設定します。|`selectPeople`|
|`setSelected`|String| 省略可能なパラメーターです。 事前に選択したユーザーの Microsoft Azure Active Directory (Azure AD) ID を渡す必要があります。 このパラメーターは、ユーザー ピッカー入力コントロールの起動中にユーザーを事前に選択します。 1 つの選択の場合、最初の有効なユーザーのみが事前設定され、残りは無視されます。|**Null**|
|`openOrgWideSearchInChatOrChannel`|Boolean| これは省略可能なパラメーターであり、TRUE に設定すると、アプリがチャットまたはチャネルに追加された場合でも、組織全体のスコープでユーザー ピッカーが起動されます。|**False**|
|`singleSelect`|Boolean|これは省略可能なパラメーターであり、TRUE に設定すると、ユーザー ピッカーが起動され、選択が 1 人のユーザーのみに制限されます。|**False**|

次の図は、モバイル デバイスとデスクトップでのユーザー ピッカーのエクスペリエンスを示しています。

# <a name="mobile"></a>[モバイル](#tab/Samplemobileapp)

ユーザー ピッカー入力コントロールを使用すると、ユーザーは次の手順を使用してユーザーを検索して追加できます。

1. 必要なユーザーの名前を入力します。 リストに名前の候補が表示されます。
1. リストから必要なユーザーの名前を選択します。

   :::image type="content" source="../../assets/images/tabs/people-picker-control-capability-mobile-updated.png" alt-text="ピッカーとピッカー モバイル":::

# <a name="desktop"></a>[デスクトップ](#tab/Sampledesktop)

Web またはデスクトップ上のユーザー ピッカー コントロールは、Web アプリの上部にあるモーダル ウィンドウで起動され、ユーザーを追加するには、次の手順を使用します。

1. 必要なユーザーの名前を入力します。 リストに名前の候補が表示されます。
1. リストから必要なユーザーの名前を選択します。

   :::image type="content" source="../../assets/images/tabs/select-people-picker-byname.png" alt-text="デスクトップ名によるユーザー ピッカー":::

---

## <a name="code-snippet"></a>コード スニペット

次のコード スニペットでは、`selectPeople` API ユーザーの使用をリストから表示します。

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

```javascript
people.selectPeople({ setSelected: ["aad id"], openOrgWideSearchInChatOrChannel: true, singleSelect: false, title: true}).then(people) => 
 {
    output(" People length: " + people.length + " " + JSON.stringify(people));
 }).catch((error) => { /*Unsuccessful operation*/ });
```

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

```javascript
people.selectPeople((error: microsoftTeams.SdkError, people: microsoftTeams.people.PeoplePickerResult[]) => 
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
  },{ setSelected: ["aad id"], openOrgWideSearchInChatOrChannel: true, singleSelect: false, title: true});
```

***

## <a name="error-handling"></a>エラー処理

次の表に、エラー コードとその説明を示します。

|エラー コード |  エラー名     | 説明|
| --------- | --------------- | --------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | API は現在のプラットフォームではサポートされていません。|
| **500** | 内部エラーです(_E) | ユーザー ピッカーの起動中に内部エラーが発生しました。|
| **4000** | 引数が無効です | API が間違った引数または不十分な必須引数で呼び出されました。|
| **8000** | USER_ABORT |ユーザーが操作を取り消しました。|
| **9000** | OLD_PLATFORM | ユーザーは、API の実装が利用できない古いプラットフォーム ビルドを使用しています。 問題を解決するには、ビルドの最新バージョンにアップグレードしてください。|

## <a name="see-also"></a>関連項目

* [メディア機能を統合する](~/concepts/device-capabilities/media-capabilities.md)
* [Teams で QR コードまたはバーコード スキャナー機能を統合する](qr-barcode-scanner-capability.md)
* [Teams で位置情報機能を統合する](location-capability.md)
