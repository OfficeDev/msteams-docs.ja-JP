---
title: アプリの計画の概要
author: heath-hamilton
description: ユース ケースと Microsoft Teams アプリの機能を理解し、ユース ケースをマップし、モバイル用の応答性の高いタブを計画します。 GCC、GCC-High、DOD の Teams の機能と可用性について説明します。
ms.topic: conceptual
ms.localizationpriority: high
ms.author: lajanuar
ms.openlocfilehash: eb72d4296ee6b91bae1775ad79eef06139abb59e
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100421"
---
# <a name="plan-your-app-with-teams-features"></a>Teams の機能を使用してアプリを計画する

優れた Teams アプリを構築することは、ユーザーのニーズを満たす適切な機能の組み合わせを見つけることです。 アプリの設計、機能は、この目的から生まれています。

At its heart, Teams is a collaboration platform. It's also a social platform, is natively cross-platform, sits at the heart of Office 365, and offers a personal canvas for you to create apps.

このセクションでは、次の方法について説明します:

* ユース ケースを特定し、Teams の機能にマップする方法。
* 計画チェックリストの使用法。
* アプリの展開以外の計画を立てる方法。

## <a name="plan-with-teams"></a>Teams で計画する

プラットフォームとしての Teams は、アプリ開発のあらゆる段階でツールキット、ライブラリ、アプリを提供します。 アプリ構築ライフサイクルに分割しましょう。

:::image type="content" source="../assets/images/app-fundamentals/plan-app.png" alt-text="アプリの計画を示す図":::

* [ビルド前](#before-you-build)
* [ビルド中](#during-build)
* [ビルド後](#post-build)
* [計画チェックリスト](../concepts/design/planning-checklist.md)

### <a name="before-you-build"></a>ビルド前

ユーザーとその懸念事項を理解することは、Teams アプリがどのように役立つかを示す最初の指標です。 問題に関するユース ケースを構築し、アプリで問題を解決する方法を決定し、ソリューションを描画します。

* **ユース ケースと Teams アプリの機能を理解する**: ユーザーの要件を理解し、適切な機能を特定できます。

* **ユース ケースのマッピング**: 共有、共同作業、ワークフロー、関連するソーシャル プラットフォームなどの要件に基づいて、一般的なユース ケースを Teams 機能にマップします。

* **Teams モバイルの応答性の高いタブを計画する**: 一般的なシナリオについて説明し、Teams モバイル用のアプリの計画に役立ちます。

### <a name="during-build"></a>ビルド中

* **アプリ プロジェクトの作成とビルド**: Teams を使用すると、アプリの要件に最適なビルド環境を選択できます。 Teams Toolkit やその他の SDK (C#、Blazor、Node.js など) を使用して作業を開始します。

* **アプリ UI のデザイン**: Teams UI Toolkit と UI ライブラリを使用してアプリのレイアウトをデザインします。

* **Teams をプラットフォームとして使用**: Teams プラットフォームを使用すると、単一または複数機能のアプリを構築できます。 Teams アプリは、アプリ エクスペリエンスを強化する統合された製品とサービスによって支えられています。

    :::image type="content" source="../assets/images/overview/teams-solution.png" alt-text="Teams ソリューションの概念表現":::

    アプリは、タブ、ボット、メッセージング拡張機能、コネクタ、Webhook として、またはマルチ機能アプリとして Teams に表示されます。 これらの機能は、タスクとプロセスの自動化に役立つ Azure、Microsoft Graph、SharePoint、Power アプリによってバックエンドに搭載されています。

    これらの機能を組み合わせることで、アプリ ソリューションが実現します。

* **デバイス機能の統合**: カメラ、QR またはバーコード スキャナー、フォト ギャラリー、マイク、位置情報などのネイティブ デバイス機能をアプリに統合できます。

### <a name="post-build"></a>ビルド後

* アプリを Teams やその他のアプリ (Microsoft 365、Microsoft Graphなど) と統合します。
* 開発者ポータルを使用して、アプリを構成、管理、デプロイします。

### <a name="government-community-cloud"></a>Government Community Cloud

Government Community Cloud (GCC) は、政府機関向けの商用環境のコピーです。 国防総省 (DOD) と連邦請負業者は、厳格なサイバーセキュリティとコンプライアンスの要件を満たす必要があります。 このため、DOD および連邦請負業者のニーズを満たすために GCC-High が作成されました。 GCC-High は DOD クラウドのコピーですが、独自の独立環境に存在します。 DOD クラウドは国防総省専用に構築されています。

次の表に、GCC、GCC-High、DOD の Teams の機能と可用性を示します。

| 機能   | GCC | GCC-High | DOD |
|-------------|---------|---|---|
| 社内で開発されたアプリと同様に、Teams が所有するアプリ | ✔️ アプリは、GCC がある場合有効です | ✔️ アプリは、GCC-High がある場合有効です | ✔️ アプリは、DOD がある場合有効です |
| Microsoft アプリ | ✔️ GCC に準拠している Microsoft アプリ | ✔️ GCC-High に準拠している Microsoft アプリ | ✔️ DOD に準拠している Microsoft アプリ |
| サードパーティ製アプリを許可する | ✔️ Third-party apps are available. Disabled by default and tenant admin use their own discretion to enable it. | ❌ | ❌ |
| ボット | ✔️ | ❌ | ❌ |
| カスタム タブ アプリまたは LOB タブ アプリ |  ✔️ | ✔️ | ✔️ |
| アプリのサイドローディング | ✔️ | ❌ | ❌ |
| カスタム ボットまたは LOB ボット | ✔️ | ❌ | ❌ |
| メッセージング拡張機能を作成する | ❌ | ❌ | ❌ |
| カスタム コネクタ | ❌ | ❌ | ❌ |

**コンプライアンス UI**: サード パーティの通信を有効にすることで、お客様はこのような通信が Microsoft ではなくサード パーティを通じて処理されることを承諾するものとします。 サービス内のサード パーティボットとの接続に関連するリスクを軽減することは、お客様ご自身の責任となります。 Microsoft は、お客様がサービスとの接続を許可する第三者のセキュリティに関して、明示または黙示を問わず、何ら保証するものではありません。 ボットを有効にすると、利用するボットに基づいて、このテナントを超えてシステム境界が拡張されます。 これが FedRAMP、DFARS、ITAR などのコンプライアンス要件を満たしていることを確認するのは、お客様の責任です。接続するエンドポイントと URL のリスクとコンプライアンスを評価するのは、お客様の責任です。

次のリストは、機能に対する GCC、GCC-High、および DOD の可用性を特定するのに役立ちます。

* サード パーティ製アプリについては、「[Web Apps](../samples/integrating-web-apps.md)」および「[会議アプリ拡張性](../apps-in-teams-meetings/meeting-app-extensibility.md)」を参照してください。
* ボットについては、「[ Teams の最初の会話ボットを構築する](../get-started/first-app-bot.md)」、「[Teams ボットの設計](../bots/design/bots.md)」、「[Microsoft Teams アプリにボットを追加する](../resources/bot-v3/bots-overview.md)」、「[Teams でのボット](../bots/what-are-bots.md)」を山荘してください。
* アプリのサイド ローディングについては、「[カスタマイズする Teams アプリを有効にする](../concepts/design/enable-app-customization.md)」、「[Microsoft Teams アプリの配布](../concepts/deploy-and-publish/apps-publish-overview.md)」、「[Teams でアプリをアップロードする](../concepts/deploy-and-publish/apps-upload.md)」を参照してください。
* カスタム コネクタについては、「[Teams 用 Office 365 コネクタの作成](../webhooks-and-connectors/how-to/connectors-creating.md)」を参照してください。

</details>

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [ユース ケースと Teams 機能](design/understand-use-cases.md)

## <a name="see-also"></a>関連項目

* [計画チェックリスト](../concepts/design/planning-checklist.md)
* [Teams 統合に関する考慮事項](../samples/integrating-web-apps.md)
* [最初の Microsoft Teams アプリを構築する](../build-your-first-app/build-first-app-overview.md)
