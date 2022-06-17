---
title: メッセージ拡張機能を開発する
description: このモジュールでは、Microsoft Teamsでメッセージ拡張機能を使用する方法について説明します。
ms.topic: overview
ms.localizationpriority: medium
ms.openlocfilehash: c81df30b71bbdba19842e45f06b4c9bb930e4c0d
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143978"
---
# <a name="develop-message-extensions-for-microsoft-teams"></a>Microsoft Teams用のメッセージ拡張機能を開発する

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

メッセージ拡張機能は、ユーザーがMicrosoft Teamsからアプリに関わる強力な方法です。 この機能を使用すると、ユーザーはサービスとの間で情報を照会または投稿し、その情報をカード形式でメッセージに直接投稿できます。

![メッセージ拡張カードの例](~/assets/images/compose-extensions/ceexample.png)

メッセージ表示オプションは、作成ボックスの下部に表示されます。 絵文字、GIF、ステッカーなど、いくつかの機能が組み込まれています。 [ **その他のオプション** (**&#8943;**)] ボタンを選択すると、アプリ ギャラリーから追加したり、自分でアップロードしたりするメッセージ拡張機能など、他のメッセージ拡張機能が表示されます。

メッセージ拡張機能を使用する方法 いくつかの可能性を次に示します。

* 作業項目とバグ。
* カスタマー サポート チケット。
* 使用状況グラフとレポート。
* 画像とメディア コンテンツ。
* 営業案件と潜在顧客。

## <a name="types-of-message-extensions"></a>メッセージ拡張機能の種類

現在Teams用に作成できるメッセージ拡張機能は、主に 2 種類あります。 次のトピックでは、それらを作成するプロセスについて説明します。

* [検索ベースのメッセージ拡張機能](~/resources/messaging-extension-v3/search-extensions.md): サービスに情報を照会し、メッセージに挿入します。 例: 作業項目を参照する
* [アクション ベースのメッセージ拡張機能](~/resources/messaging-extension-v3/create-extensions.md): ユーザーから情報を収集し、サード パーティのサービスに投稿します。 例: 作業項目を作成する
