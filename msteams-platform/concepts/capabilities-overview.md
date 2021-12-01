---
title: アプリの機能を理解する
author: heath-hamilton
description: タブ、Teamsメッセージング拡張機能、Webhooks およびコネクタなどのアプリ機能の説明。
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: lajanuar
ms.date: 09/22/2020
keywords: tabss bots メッセージング拡張機能 webhooks コネクタ gcc
ms.openlocfilehash: 9b60556fce448eeecb1f3b96460ea53c8abd5be5
ms.sourcegitcommit: 5df8c1013005305996e8ded3538e2b5845352720
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/01/2021
ms.locfileid: "61246079"
---
# <a name="understand-microsoft-teams-app-capabilities"></a>アプリMicrosoft Teamsについて

機能拡張またはエントリ ポイントは、アプリがユーザーに表示されるさまざまな方法です。 たとえば、ユーザーはキャンバス タブでアプリを操作してアクティビティを実行したり、会話型ボットを使用して同じ操作を行う場合があります。 アプリの作成に使用されるさまざまな機能Teams使用範囲を拡大できます。

アプリを拡張する方法は複数Teams、すべてのアプリが一意です。 Webhook などの機能は 1 つのみ、ユーザーにさまざまなオプションを提供する複数の機能を備える機能もあります。 たとえば、アプリは、データを中央の場所 (タブ) に表示し、会話インターフェイス (ボット) を介して同じ情報を表示 **できます**。

## <a name="app-capabilities"></a>アプリの機能

アプリTeams、次のコア機能の 1 つまたはすべてが含まれます。

* [タブ](../tabs/what-are-tabs.md)
* [メッセージング拡張機能](../messaging-extensions/what-are-messaging-extensions.md)
* [ボット](../bots/what-are-bots.md)
* [Webhook とコネクタ](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)

また、アプリは、Microsoft Graph API などの高度な機能[を利用Teams。](/graph/teams-concept-overview)

次の図は、アプリで必要な機能を提供する機能を示しています。

:::image type="content" source="../assets/images/capabilities-overview.png" alt-text="アプリの機能のTeamsを示すマインド マップ。":::

## <a name="always-consider-your-user"></a>ユーザーを常に考慮する

アプリ開発に関するTeams理解すると、その基本的な基礎を理解できます。 特定の機能を構築する方法は複数あると理解しています。 このようなシナリオでは、ユーザーによりネイティブなエクスペリエンスを提供する方法を検討してください。
たとえば、アプリ内のタブとして構築されたフォームでユーザー入力を収集できます。 また、ビューを切り替えてユーザーのワークフローを中断することなく、タスク モジュールを使用してこれを実行できます。 ユーザーの通常のワークフローからの偏差を最も少ない拡張ポイントを選択することが重要です。

## <a name="government-community-cloud-gcc"></a>Government Community Cloud (GCC)

Government Community Cloudは、商用環境の政府に焦点を当てたコピーです。 国防総省 (DOD) と連邦の請負業者は、厳しいサイバーセキュリティとコンプライアンス要件を満たす必要があります。 このために、DOD GCC-High連邦の請負業者のニーズを満たすために作成されたサービスです。 GCC-High DOD クラウドのコピーですが、独自の主権環境に存在します。 DOD クラウドは国防総省専用に構築されています。

> [!NOTE]
> Teamsが進化しました。
> 
> 以前は、タイルの省略記号を選択して LOB アプリが更新されました。 更新されたストア エクスペリエンスTeams、管理センターにログインして LOB アプリ[を更新Teamsできます](https://admin.teams.microsoft.com)。

次の表に、Teams、GCC-High、DOD のGCC機能と可用性を示します。

| 機能   | GCC | GCC-High | DOD |
|-------------|---------|
| Teams開発されたアプリと同様に、所有するアプリを管理する | ✔️アプリが有効になっている場合はGCC。 | ✔️が高い場合は、アプリGCC有効になります。 | ✔️ DOD がある場合は、アプリが有効になります。 |
| Microsoft アプリ | ✔️に準拠した Microsoft アプリGCC | ✔️に準拠した Microsoft アプリGCC-High | ✔️ Microsoft アプリが DOD に準拠している場合 |
| 3p またはサード パーティ製アプリ | ✔️サード パーティ製アプリを利用できます。 既定では無効になり、テナント管理者は独自の裁量を使用して有効にします。 | ❌ | ❌ |
| ボット | ✔️ | ❌ | ❌ |
| カスタム または Lob タブ アプリ |  ✔️ | ✔️ | ✔️ |
| サイドローディング アプリ | ✔️ | ❌ | ❌ |
| カスタム ボットまたは Lob ボット | ✔️ | ❌ | ❌ |
| カスタム メッセージング拡張機能 | ❌ | ❌ | ❌ |
| カスタム コネクタ | ❌ | ❌ | ❌ |

次の一覧は、機能の GCC、GCC-高、DOD の可用性を識別するのに役立ちます。

* サード パーティ製アプリについては [、「Web アプリと会議](../samples/integrating-web-apps.md) アプリの機能拡張」 [を参照してください](../apps-in-teams-meetings/meeting-app-extensibility.md)。
* ボットについては[、「Teams](../get-started/first-app-bot.md)用の最初の会話型ボットの構築、Teams ボットの設計[、Microsoft Teams](../bots/design/bots.md)アプリへの[](../resources/bot-v3/bots-overview.md)ボットの追加、Teams でのボットの追加[」をご覧ください](../bots/what-are-bots.md)。
* サイドローディング アプリについては[、「Teams](../concepts/design/enable-app-customization.md)アプリをカスタマイズする、Microsoft Teams アプリを配布[](../concepts/deploy-and-publish/apps-publish-overview.md)する、アップロード アプリをカスタマイズする」を参照[Teams。](../concepts/deploy-and-publish/apps-upload.md)
* カスタム コネクタについては、「create [Office 365 コネクタ」を参照Teams。](../webhooks-and-connectors/how-to/connectors-creating.md)

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [Teams アプリのエントリ ポイント](../concepts/extensibility-points.md)

## <a name="see-also"></a>関連項目

* [アプリのビルド Teams](../overview.md)
* [最初のアプリをMicrosoft Teamsする](../build-your-first-app/build-first-app-overview.md)