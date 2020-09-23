---
title: Teams アプリの機能について
author: heath-hamilton
description: Teams アプリの機能の説明
ms.topic: conceptual
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: e7a6fe61fa5c74547ce20cc895afdd044f35e512
ms.sourcegitcommit: 1aa0b172931d0f81db346452788c41dc4a6717b9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "48210276"
---
# <a name="understanding-teams-app-capabilities"></a>Teams アプリの機能について

*機能* は、Microsoft Teams プラットフォームでアプリを作成するための拡張点です。

Teams を拡張する方法は複数ありますが、すべてのアプリが一意であるため、一部のアプリは1つの機能 (webhook など) しか持たないため、ユーザーのオプションを提供する方法がいくつかあります。 たとえば、アプリではデータを中央の場所 (タブ) に表示し、会話インターフェイス (bot) を通じて同じ情報を表示することができます。

Teams アプリには、次のコア機能のいずれかまたはすべてを含めることができます。

* [タブ](../tabs/what-are-tabs.md)
* [メッセージング拡張機能](../messaging-extensions/what-are-messaging-extensions.md)
* [ボット](../bots/what-are-bots.md)
* [Webhook とコネクタ](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)

アプリでは、 [Microsoft GRAPH API For Teams](https://docs.microsoft.com/graph/teams-concept-overview)などの高度な機能を利用することもできます。

アプリに必要な機能を提供する機能については、次の図を参照してください。

:::image type="content" source="../assets/images/capabilities-overview.png" alt-text="Teams アプリの機能についてのマインドマップ。":::

## <a name="doing-whats-best-for-your-users"></a>ユーザーにとって最適な方法

Teams アプリの開発について理解すると、その微妙な違いについて理解し始められます。 特定の機能 (ユーザー入力の収集など) を構築する方法は複数あります。 たとえば、を使用して、web ベースのフォームをタブに埋め込むことができ `<iframe>` ます。 また、タスクモジュールである Teams の UI 規則を使用して、ユーザーが望むようによりネイティブな操作を行うことができるタブで、これを行うこともできます。

適切な機能と設計を選択することによって、最初に [対象ユーザーのユースケースを理解](../concepts/design/understand-use-cases.md)します。
