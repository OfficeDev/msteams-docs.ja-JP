---
title: メッセージング拡張機能の開発
description: メッセージング拡張機能の使用を開始する方法について説明Microsoft Teams
ms.topic: overview
ms.localizationpriority: medium
keywords: teams メッセージング拡張機能メッセージング拡張機能
ms.openlocfilehash: ea07ae8c7a7a16f5187adfe6dbe5f52d8bf47056
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2021
ms.locfileid: "59156515"
---
# <a name="develop-messaging-extensions-for-microsoft-teams"></a>ユーザーのメッセージング拡張機能を開発Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

メッセージング拡張機能は、ユーザーがユーザーからアプリに参加するための強力なMicrosoft Teams。 この機能を使用すると、ユーザーはサービスとの間で情報を照会または投稿し、その情報をカード形式でメッセージに投稿できます。

![メッセージング拡張機能カードの例](~/assets/images/compose-extensions/ceexample.png)

メッセージング拡張機能は、作成ボックスの下部に表示されます。 絵文字、Giphy、ステッカーなど、いくつか組み込みです。 [その **他のオプション** ]**(&#8943;**) ボタンを選択すると、アプリ ギャラリーから追加したり、自分でアップロードしたりしたメッセージング拡張機能を表示できます。

メッセージング拡張機能の使い方 いくつかの可能性を次に示します。

* 作業項目とバグ
* カスタマー サポート チケット
* 使用状況グラフとレポート
* 画像とメディア コンテンツ
* 営業案件とリード

## <a name="types-of-messaging-extensions"></a>メッセージング拡張機能の種類

現在のユーザーに対して作成できるメッセージング拡張機能は、主に 2 Teamsです。 次のトピックでは、作成プロセスについて説明します。

* [検索ベースのメッセージング拡張機能](~/resources/messaging-extension-v3/search-extensions.md): サービスに情報を照会し、メッセージに挿入します。 例: 作業項目を参照する
* [アクション ベースのメッセージング拡張機能](~/resources/messaging-extension-v3/create-extensions.md): ユーザーから情報を収集し、サードパーティ サービスに投稿します。 例: 作業項目の作成
