---
title: メッセージング拡張機能の開発
description: Microsoft Teams でのメッセージング拡張機能の使用を開始する方法について説明します。
ms.topic: overview
keywords: teams メッセージング拡張機能メッセージング拡張機能
ms.openlocfilehash: 1eb75371b1a8adbeadbcbdbc0d06c7d88f2f1ccc
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696550"
---
# <a name="develop-messaging-extensions-for-microsoft-teams"></a>Microsoft Teams のメッセージング拡張機能を開発する

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

メッセージング拡張機能は、ユーザーが Microsoft Teams からアプリに参加するための強力な方法です。 この機能を使用すると、ユーザーはサービスとの間で情報を照会または投稿し、その情報をカード形式でメッセージに投稿できます。

![メッセージング拡張機能カードの例](~/assets/images/compose-extensions/ceexample.png)

メッセージング拡張機能は、作成ボックスの下部に表示されます。 絵文字、Giphy、ステッカーなど、いくつか組み込みです。 [その **他のオプション** ]**(&#8943;**) ボタンを選択すると、アプリ ギャラリーから追加したり、自分でアップロードしたりしたメッセージング拡張機能を表示できます。

メッセージング拡張機能の使い方 いくつかの可能性を次に示します。

* 作業項目とバグ
* カスタマー サポート チケット
* 使用状況グラフとレポート
* 画像とメディア コンテンツ
* 営業案件とリード

## <a name="types-of-messaging-extensions"></a>メッセージング拡張機能の種類

Teams 用に作成できるメッセージング拡張機能は、主に 2 種類あります。 次のトピックでは、作成プロセスについて説明します。

* [検索ベースのメッセージング拡張機能](~/resources/messaging-extension-v3/search-extensions.md): サービスに情報を照会し、メッセージに挿入します。 例: 作業項目を参照する
* [アクション ベースのメッセージング拡張機能](~/resources/messaging-extension-v3/create-extensions.md): ユーザーから情報を収集し、サードパーティ サービスに投稿します。 例: 作業項目の作成
