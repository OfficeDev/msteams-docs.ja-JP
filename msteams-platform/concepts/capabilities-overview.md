---
title: アプリの機能を理解する
author: heath-hamilton
description: Teams アプリの機能の説明
ms.topic: conceptual
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 6d08d06c55aed4b531fba4bb533c896c13073cfc
ms.sourcegitcommit: 9404c2e3a30887b9e17e0c89b12dd26fd9b8033e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/09/2021
ms.locfileid: "51654434"
---
# <a name="understand-microsoft-teams-app-capabilities"></a>Microsoft Teams アプリの機能について

機能拡張またはエントリ ポイントは、アプリがユーザーに表示されるさまざまな方法です。 たとえば、ユーザーはキャンバス タブでアプリを操作してアクティビティを実行したり、会話型ボットを使用して同じ操作を行う場合があります。 Teams アプリの構築に使用されるさまざまな機能を使用すると、使用範囲を拡大できます。

Teams を拡張する方法は複数あるので、すべてのアプリは一意です。 Webhook などの機能は 1 つのみ、ユーザーにさまざまなオプションを提供する複数の機能を備える機能もあります。 たとえば、アプリは、データを中央の場所 (タブ) に表示し、会話インターフェイス (ボット) を介して同じ情報を表示 **できます**。

## <a name="app-capabilities"></a>アプリの機能

Teams アプリには、次のコア機能の 1 つまたはすべてが含まれます。

* [タブ](../tabs/what-are-tabs.md)
* [メッセージング拡張機能](../messaging-extensions/what-are-messaging-extensions.md)
* [ボット](../bots/what-are-bots.md)
* [Webhook とコネクタ](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)

アプリでは、Microsoft Graph API for Teams などの高度な [機能を利用することもできます](https://docs.microsoft.com/graph/teams-concept-overview)。

次の図は、アプリで必要な機能を提供する機能を示しています。

:::image type="content" source="../assets/images/capabilities-overview.png" alt-text="Teams アプリの機能を示すマインド マップ。":::

## <a name="always-consider-your-user"></a>ユーザーを常に考慮する

Teams アプリの開発に慣れ親しんだら、その基本的な基本を理解できます。 特定の機能を構築する方法は複数あると理解しています。 このようなシナリオでは、ユーザーによりネイティブなエクスペリエンスを提供する方法を検討してください。
たとえば、アプリ内のタブとして構築されたフォームでユーザー入力を収集できます。 また、ビューを切り替え、ユーザーの作業フローを中断することなく、タスク モジュールを使用してこれを実行できます。 ユーザーの通常の作業フローから最も逸脱しない拡張ポイントを選択することが重要です。

## <a name="see-also"></a>関連項目

> [!div class="nextstepaction"]
> [Teams 用アプリのビルド](../overview.md)
## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [Teams アプリのエントリ ポイント](../concepts/extensibility-points.md)
