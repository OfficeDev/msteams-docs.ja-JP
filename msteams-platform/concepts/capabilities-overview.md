---
title: Teams アプリの機能について
author: heath-hamilton
description: Teams アプリの機能の説明
ms.topic: conceptual
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 5336b36b52cf81be414f18ccaaf9e235c079e626
ms.sourcegitcommit: 49d1ecda14042bf3f368b14c1971618fe979b914
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/23/2021
ms.locfileid: "51034706"
---
# <a name="understanding-teams-app-capabilities"></a>Teams アプリの機能について

*機能は* 、Microsoft Teams プラットフォームでアプリを構築する拡張ポイントです。

Teams を拡張する方法は複数あるので、すべてのアプリは一意です。一部のアプリには 1 つの機能 (webhook など) しか持てない場合と、ユーザーにオプションを提供する機能がいくつかあります。 たとえば、アプリは中央の場所 (タブ) にデータを表示し、会話インターフェイス (ボット) を通じて同じ情報を表示できます。

Teams アプリには、次のコア機能の 1 つまたはすべてが含まれます。

* [タブ](../tabs/what-are-tabs.md)
* [メッセージング拡張機能](../messaging-extensions/what-are-messaging-extensions.md)
* [ボット](../bots/what-are-bots.md)
* [Webhook とコネクタ](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)

アプリでは、Microsoft Graph API for Teams などの高度な [機能を利用することもできます](https://docs.microsoft.com/graph/teams-concept-overview)。

アプリで必要な機能を提供する機能を確認するには、次の図を参照してください。

:::image type="content" source="../assets/images/capabilities-overview.png" alt-text="Teams アプリの機能を示すマインド マップ。":::

## <a name="doing-whats-best-for-your-users"></a>ユーザーに最適な機能を実行する

Teams アプリの開発に慣れ親しんだら、その微妙な点を理解し始めるでしょう。 特定の機能 (ユーザー入力の収集など) を作成する方法は複数ある。 たとえば、Web ベースのフォームをタブに埋め込むには、 を使用します `<iframe>` 。 また、ユーザーが優先するよりネイティブなエクスペリエンスを得る場合は、タスク モジュールである Teams UI 規則を使用してタブでこれを実行することもできます。

適切な機能と設計を選ぶには、まず対象ユーザーの使用例 [を理解する必要があります](../concepts/design/understand-use-cases.md)。
