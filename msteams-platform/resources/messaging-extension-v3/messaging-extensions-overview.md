---
title: メッセージ拡張機能を開発する
description: Microsoft Teamsでメッセージ拡張機能を使用する方法について説明します
ms.topic: overview
ms.localizationpriority: medium
keywords: teams メッセージング拡張機能メッセージング拡張機能
ms.openlocfilehash: 8d44ea8ffe3c265a5c65ae2e842fe4f55f950e58
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111921"
---
# <a name="develop-message-extensions-for-microsoft-teams"></a>Microsoft Teams用のメッセージ拡張機能を開発する

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

メッセージ拡張機能は、ユーザーがMicrosoft Teamsからアプリに関わる強力な方法です。 この機能を使用すると、ユーザーはサービスとの間で情報を照会または投稿し、その情報をカード形式でメッセージに直接投稿できます。

![メッセージ拡張カードの例](~/assets/images/compose-extensions/ceexample.png)

メッセージ表示オプションは、作成ボックスの下部に表示されます。 絵文字、Giphy、ステッカーなど、いくつかの機能が組み込まれています。 [ **その他のオプション** (**&#8943;**)] ボタンを選択すると、アプリ ギャラリーから追加したり、自分でアップロードしたりするメッセージ拡張機能など、他のメッセージ拡張機能が表示されます。

メッセージ拡張機能を使用する方法 いくつかの可能性を次に示します。

* 作業項目とバグ
* カスタマー サポート チケット
* 使用状況グラフとレポート
* 画像とメディア コンテンツ
* 営業案件と潜在顧客

## <a name="types-of-message-extensions"></a>メッセージ拡張機能の種類

現在Teams用に作成できるメッセージ拡張機能は、主に 2 種類あります。 次のトピックでは、それらを作成するプロセスについて説明します。

* [検索ベースのメッセージ拡張機能](~/resources/messaging-extension-v3/search-extensions.md): サービスに情報を照会し、メッセージに挿入します。 例: 作業項目を参照する
* [アクション ベースのメッセージ拡張機能](~/resources/messaging-extension-v3/create-extensions.md): ユーザーから情報を収集し、サード パーティのサービスに投稿します。 例: 作業項目を作成する
