---
title: アプリの機能を理解する
author: heath-hamilton
description: Teams機能の説明
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 209d187681b1370440931fcd40744965395b13e8
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565152"
---
# <a name="understand-microsoft-teams-app-capabilities"></a>アプリMicrosoft Teamsについて

機能拡張またはエントリ ポイントは、アプリがユーザーに表示されるさまざまな方法です。 たとえば、ユーザーはキャンバス タブでアプリを操作してアクティビティを実行したり、会話型ボットを使用して同じ操作を行う場合があります。 アプリの構築に使用されるさまざまな機能Teams使用範囲を拡大できます。

アプリを拡張する方法は複数Teams、すべてのアプリが一意です。 Webhook などの機能は 1 つのみ、ユーザーにさまざまなオプションを提供する複数の機能を備える機能もあります。 たとえば、アプリは、データを中央の場所 (タブ) に表示し、会話インターフェイス (ボット) を介して同じ情報を表示 **できます**。

## <a name="app-capabilities"></a>アプリの機能

アプリTeams、次のコア機能の 1 つまたはすべてがあります。

* [タブ](../tabs/what-are-tabs.md)
* [メッセージング拡張機能](../messaging-extensions/what-are-messaging-extensions.md)
* [ボット](../bots/what-are-bots.md)
* [Webhook とコネクタ](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)

また、アプリは、Microsoft Graph API などの高度な機能[を利用Teams。](/graph/teams-concept-overview)

次の図は、アプリで必要な機能を提供する機能を示しています。

:::image type="content" source="../assets/images/capabilities-overview.png" alt-text="アプリの機能のTeamsを示すマインド マップ。":::

## <a name="always-consider-your-user"></a>ユーザーを常に考慮する

アプリ開発に関するTeams理解すると、その基本的な基礎を理解できます。 特定の機能を構築する方法は複数あると理解しています。 このようなシナリオでは、ユーザーによりネイティブなエクスペリエンスを提供する方法を検討してください。
たとえば、アプリ内のタブとして構築されたフォームでユーザー入力を収集できます。 また、ビューを切り替え、ユーザーの作業フローを中断することなく、タスク モジュールを使用してこれを実行できます。 ユーザーの通常の作業フローから最も逸脱しない拡張ポイントを選択することが重要です。

## <a name="see-also"></a>関連項目

[アプリのビルド Teams](../overview.md)

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [Teams アプリのエントリ ポイント](../concepts/extensibility-points.md)
