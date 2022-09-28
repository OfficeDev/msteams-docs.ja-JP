---
title: Microsoft Teams プラットフォーム用のアプリを構築する
author: heath-hamilton
description: Microsoft Teams、Teams プラットフォームでアプリを構築する理由、Teams アプリがビジネス ニーズを満たす方法について説明します。
ms.topic: overview
ms.localizationpriority: high
ms.author: lajanuar
ms.date: 05/24/2021
ms.openlocfilehash: 143f316a6f5153185e78b2efa4ec1db3dc9c1fa6
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100204"
---
# <a name="teams-app-that-fits"></a>最適な Teams アプリ

Microsoft Teams では、Microsoft または外部のサービスによって提供されるアプリのコレクションが用意されています。 Teams アプリは、タブ、ボット、メッセージ拡張機能、またはこれら 3 つの任意の組み合わせです。 これらのアプリは、Teams での共同作業エクスペリエンスの価値を向上させます。

Apps can be personal or shared. A personal app enables a one-on-one communication, and a shared app lets multiple users share app space to collaborate.

## <a name="driving-organizational-goals"></a>組織の目標を推進する

Collaboration and communication are key for an organization. Concise communication, integration with necessary services, and on-the-go accessibility is why organizations are increasingly choosing to rely on apps.

組織は、顧客とつながり、サービスを提供し、情報を共有するためにアプリを使用します。 しかし、これだけではありません。 アプリは、ユーザーが一緒に作業するために集まる場所です。 よく配置されたアプリは、社外および社内のビジネス ニーズに合った統一感のある環境を構築するのに役立ちます。

アプリがどのような分野でビジネス ニーズを満たすのに役立つかを見てみましょう。

:::image type="content" source="../msteams-platform/assets/images/overview/why-teams-apps.png" alt-text="Teams アプリを構築する理由":::

| **開発オプション** | **ビジネス チャンス** |
| --- | --- |
| - デスクトップ アプリ <br> - Web アプリ <br> - モバイル アプリ | - ユーザー エンゲージメントを増やす <br> - アプリを Teams ストアで検出できるようにする |
| **顧客のメリット** | **社内ワークフロー** |
| - 外出先でのアクセシビリティ <br> - 顧客データのセキュリティ保護 <br> - 簡単にできるコミュニケーション | - 反復的なタスクの自動化 <br> - Q&A やヘルプデスクなどの <br> &nbsp;&nbsp; タスクをボットで簡略化する |

Teams 開発者プラットフォームで、ニーズに合わせて Teams 機能を拡張することで、アプリを構築できます。 Teams 用に新しいものを作成するか、既存のアプリを統合します。

## <a name="build-apps-with-microsoft-teams-platform"></a>Microsoft Teams プラットフォームでアプリを構築する

Teams アプリは、重要な情報、共通のツール、信頼できるプロセスを提供することで、コラボレーション ワークスペースの生産性を向上させ、ユーザーが集まり、学習し、仕事をする場を増やします。 アプリは、要件に合わせて Teams プラットフォームの機能を拡張する方法です。 新しいアプリを作成するか、既存のアプリを統合して、特定のビジネス ニーズに合わせて Teams プラットフォームの利点を活用します。

アプリを構築することの利点は、組織の目標の達成や社内の生産性の向上まで、さまざまです。

Teams がアプリのニーズに最適である理由は次のとおりです。

- **コミュニケーションおよびコラボレーション**

    Most successful Teams apps involve pulling information from another system, having a conversation about it, and letting users to take action. Teams lets you do all these tasks directly within the Teams client. You can even push information to a targeted audience based on an event or action in an external system.

- **ソーシャルなやり取り**

    Teams はソーシャル プラットフォームです。交流を重視したカスタム アプリを使用することで、チームは社内文化を共同作業の場に広げることができます。 アプリを使用して投票を送信し、ユーザーが互いにフィードバックを共有し、つながりとコミュニケーションを可能にします。

    :::image type="content" source="../msteams-platform/assets/images/overview/teams-apps-social.png" alt-text="チームの文化を構築するために Teams アプリを使用する":::

- **一般的なビジネス プロセス**

    Tasks like creating and sharing a sales call report, tracking your project timeline, reserving common resources, submitting help desk requests are repetitive tasks. They make for effective Teams apps.

    アプリは、反復的なワークフローの自動化だけでなく、コミュニケーションの問題を解決することにも役立ちます。 チャット ボットは、IT 部門または人事部門へのメールや電話を簡単に置き換えることのできる機能です。

    :::image type="content" source="../msteams-platform/assets/images/overview/teams-apps-bot.png" alt-text="社内使用のための Teams アプリ":::

- **Teams ストアの利点**

    アプリを Teams ストアにプッシュしてアプリの可用性を向上させると、マーケティングの機会として利用できます。 新規事業を運営している場合、Teams プラットフォームは製品の認知度を高めるのに役立ちます。 Teams ストア マーケットプレースは、多くの対象ユーザーがアプリを見つけるための優れたプラットフォームです。

- **既存のアプリの露出を高める**

    既存の Web アプリ、SharePoint サイト (または SPFx 拡張機能)、PowerApp、またはその他の Web ベースのアプリケーションがある場合、それらの一部またはすべての Teams で有効にすることが効果的な場合があります。 Teams に既存のアプリを拡張し、対話機能を移植すると、アプリのユーザー ベースとユーザー エンゲージメントを向上させるのに役立ちます。

    :::image type="content" source="../msteams-platform/assets/images/overview/teams-apps-sp.png" alt-text="Teams タブとして移植された SharePoint タブ":::

- **タブとボットを使用した個人用アプリ**

    1 対 1 の会話ボットは、Teams の機能の中でも自由度の高い機能です。 ボットとユーザーの間でのみ会話が行われます。 タスク モジュールを柔軟に組み込み、複雑な情報のセットを簡略化できます。

    たとえば、アプリが複数の共同作業者が使用するデザイン ツールである場合、すべてのユーザーに通知する共有ボットは、ユーザー エンゲージメントを構築するのに役立ちます。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [アイデアを Teams アプリに活用する](overview-story.md)
