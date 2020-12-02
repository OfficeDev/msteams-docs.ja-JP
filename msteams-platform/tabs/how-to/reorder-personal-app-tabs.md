---
title: 個人用アプリのタブの順序を変更する
description: 個人用アプリで個人用アプリの静的タブの順序を変更する方法
keywords: teams タブの開発
ms.openlocfilehash: a8a7c3d23bac98ef1085a8f3443ca0fc92ae0a31
ms.sourcegitcommit: bfdcd122b6b4ffc52d92320d4741f870c07f0542
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2020
ms.locfileid: "49554830"
---
# <a name="reorder-personal-app-tabs"></a>個人用アプリのタブの順序を変更する

マニフェストバージョン1.7 の開発者は、個人用アプリのすべてのタブを再配置できます。 特に、開発者は、[個人情報] タブヘッダー内の任意の場所にある "bot チャット" タブ (常に最初の位置に既定で指定されています) を移動することができます。 2つの予約済みタブ entityId キーワードを宣言しました。「会話」と「about」。

## <a name="moving-the-chatconversation-tab"></a>[チャット/会話] タブの移動

"Personal" スコープを持つ bot を作成すると、パーソナルアプリの最初のタブ位置に常に表示されます。 別の位置に移動する場合は、予約済みのキーワード "会話" を使用して、静的な tab オブジェクトをマニフェストに追加する必要があります。 「StaticTabs」配列に [会話] タブを追加すると、web とデスクトップに [会話] タブが表示されます。 

```json
{
   "staticTabs":[
      {
         
      },
      {
         "entityId":"conversations",
         "scopes":[
            "personal"
         ]
      }
   ]
}
```

> [!NOTE]
> 個人用の bot チャットには、個人用アプリ内に専用の場所があるため、この動作はモバイルには反映されていないことに注意してください。

## <a name="moving-the-about-tab"></a>[バージョン情報] タブの移動

[About] タブは、常に [個人用アプリ] タブのヘッダーバーの末尾に表示されます。 別の位置に移動する場合は、"about" entityId を使用する必要があります。

```json
{
   "staticTabs":[
      {
         
      },
      {
         "entityId":"about",
         "scopes":[
            "personal"
         ]
      }
   ]
}
```
> [!NOTE]
> [バージョン情報] タブは、モバイルでは表示されません。

## <a name="example-code"></a>コード例

```json
{
   "staticTabs":[
      {
         "entityId":"homeTab",
         "name":"Home",
         "contentUrl":"https://www.contoso.com",
         "websiteUrl":" https://www.contoso.com ",
         "scopes":[
            "personal"
         ]
      },
      {
         "entityId":"about",
         "scopes":[
            "personal"
         ]
      },
      {
         "entityId":"conversations",
         "scopes":[
            "personal"
         ]
      }
   ]
}
```
