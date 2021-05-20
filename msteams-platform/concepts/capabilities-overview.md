---
title: アプリの機能について
author: heath-hamilton
description: Teamsアプリの機能について説明
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
# <a name="understand-microsoft-teams-app-capabilities"></a>アプリの機能Microsoft Teams理解する

機能拡張やエントリ ポイントは、アプリがユーザーに対してマニフェストを作成する方法が異なります。 たとえば、ユーザーがキャンバス タブでアプリを操作してアクティビティを実行したり、会話型ボットを使用して同じ操作を行ったりできます。 Teams アプリの構築に使用するさまざまな機能により、その使用範囲を拡大できます。

Teams拡張する方法は複数あるので、すべてのアプリは一意です。 Webhook などの機能は 1 つしかない場合もあれば、ユーザーにさまざまなオプションを提供する機能が複数あるものもあります。 たとえば、アプリは、データを中央の場所、つまり **タブ** に表示し、会話型インターフェイス、つまり **ボット** を通じて同じ情報を表示できます。

## <a name="app-capabilities"></a>アプリの機能

Teamsアプリには、次のコア機能のいずれかまたはすべてが含まれます。

* [タブ](../tabs/what-are-tabs.md)
* [メッセージング拡張機能](../messaging-extensions/what-are-messaging-extensions.md)
* [ボット](../bots/what-are-bots.md)
* [Webhook とコネクタ](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)

アプリは[、Teams用](/graph/teams-concept-overview)の Microsoft Graph API などの高度な機能を利用することもできます。

次の図は、アプリで必要な機能を提供する機能を示しています。

:::image type="content" source="../assets/images/capabilities-overview.png" alt-text="アプリの機能Teams示すマインドマップ。":::

## <a name="always-consider-your-user"></a>常にユーザーを考慮する

アプリ開発に慣れTeams、その基本を理解します。 特定の機能を構築する方法が複数あることを理解しています。 このようなシナリオでは、ユーザーによりネイティブなエクスペリエンスを提供する方法を検討してください。
たとえば、アプリのタブとして作成されたフォームでユーザー入力を収集できます。 また、ビューを切り替え、ユーザーの作業フローを中断することなく、タスク モジュールを使用してこれを行うこともできます。 ユーザーの通常の作業フローからの偏差を最小限にする拡張ポイントを選択することが重要です。

## <a name="see-also"></a>関連項目

[Teams用のアプリを構築する](../overview.md)

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [Teams アプリのエントリ ポイント](../concepts/extensibility-points.md)
