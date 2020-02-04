---
title: メッセージング拡張機能を開発する
description: Microsoft Teams でのメッセージング拡張機能の使用を開始する方法について説明します。
keywords: teams メッセージング拡張メッセージング拡張機能
ms.openlocfilehash: 6ba8f73d40f795a83f28707ef89c207c5d51d67c
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674651"
---
# <a name="develop-messaging-extensions-for-microsoft-teams"></a>Microsoft Teams のメッセージング拡張機能を開発する

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

メッセージング拡張機能は、ユーザーが Microsoft Teams からアプリを利用できるようにするための強力な手段です。 この機能を使用すると、ユーザーはサービスとの間で情報を照会したり、その情報をカード形式でメッセージに投稿したりできます。

![メッセージング拡張カードの例](~/assets/images/compose-extensions/ceexample.png)

メッセージング拡張機能は、[新規作成] ボックスの下部に表示されます。 絵文字、Giphy、ステッカーなどのいくつかのが組み込まれています。 [その他の**オプション**(**&#8943;**)] ボタンをクリックして、他のメッセージング拡張機能 (アプリギャラリーから追加したものや自分でアップロードしたものなど) を表示します。

メッセージング拡張機能の使用方法 いくつかの可能性があります。

* 作業項目とバグ
* カスタマーサポートチケット
* 使用状況のグラフとレポート
* 画像とメディアコンテンツ
* 営業案件と潜在顧客

## <a name="types-of-messaging-extensions"></a>メッセージング拡張機能の種類

チーム向けに作成できるメッセージング拡張機能には、主に2つの種類があります。 次のトピックでは、これらの作成手順について説明します。

* [検索ベースのメッセージング拡張](~/resources/messaging-extension-v3/search-extensions.md): サービスに情報を照会して、それをメッセージに挿入します。 例: 作業項目を検索する
* [アクションベースのメッセージング拡張](~/resources/messaging-extension-v3/create-extensions.md): ユーザーから情報を収集し、サードパーティのサービスに投稿します。 例: 作業項目を作成する
